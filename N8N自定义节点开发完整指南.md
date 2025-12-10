# N8N自定义节点开发完整指南

> **教程理念**：本教程通过一个完整的股票API节点开发案例，手把手教你如何从零开始创建N8N自定义节点，包括Credential管理、多API支持、统一输出格式等核心技能。

---

## 问题引入

当你使用N8N时，可能会遇到这样的场景：你需要调用某个API，但N8N中没有现成的节点；或者你需要调用多个类似的API（比如不同的股票数据API），但它们的认证方式和输出格式各不相同，你希望创建一个统一的节点来处理这些差异。

比如，你想要创建一个股票数据查询节点，支持多个股票API提供商（如Alpha Vantage、Finnhub、Polygon.io），每个API都有自己的API Key，但最终输出的数据格式要统一。这样，无论使用哪个API，后续的工作流节点都能以相同的方式处理数据。

这就是自定义节点的价值所在。通过创建自定义节点，你可以：
- **封装复杂逻辑**：将API调用、数据处理等逻辑封装在节点中
- **统一接口**：即使底层使用不同的API，也能提供统一的输入输出接口
- **复用代码**：一次开发，多处使用
- **增强功能**：添加N8N原生节点没有的功能

本教程将通过开发一个**股票数据查询节点**的完整案例，带你从零开始掌握N8N自定义节点的开发技能。

---

## 核心概念

### 什么是N8N自定义节点？

**自定义节点（Custom Node）**是N8N中允许开发者创建自己的节点类型的功能。它允许你：
- 定义节点的输入输出
- 定义节点的配置选项
- 定义节点的执行逻辑
- 定义节点的认证方式（Credential）

**类比理解**：
- **原生节点**：就像N8N提供的标准积木块
- **自定义节点**：就像你自己设计和制作的积木块，可以按照你的需求定制

### 自定义节点的组成部分

一个完整的自定义节点包含以下部分：

| 组成部分 | 说明 | 文件位置 |
|---------|------|---------|
| **节点定义** | 定义节点的名称、描述、图标、属性等 | `nodes/YourNode/YourNode.node.json` |
| **节点代码** | 实现节点的执行逻辑 | `nodes/YourNode/YourNode.ts` |
| **Credential定义** | 定义节点的认证方式 | `credentials/YourCredential/YourCredential.credentials.ts` |
| **节点描述** | 节点的详细说明文档 | `nodes/YourNode/YourNode.description.md` |

### 开发环境要求

在开始之前，确保你具备以下环境：

| 要求 | 说明 | 版本要求 |
|------|------|---------|
| **Node.js** | JavaScript运行环境 | >= 16.0.0 |
| **npm** | 包管理器 | >= 7.0.0 |
| **TypeScript** | 类型安全的JavaScript | >= 4.0.0 |
| **Git** | 版本控制工具 | 最新版本 |
| **代码编辑器** | VS Code推荐 | 最新版本 |

### 案例需求分析

我们的案例是创建一个**股票数据查询节点**，具体需求如下：

**功能需求**：
1. 支持多个股票API提供商（Alpha Vantage、Finnhub、Polygon.io）
2. 每个API需要不同的API Key进行认证
3. 用户可以在节点中选择使用哪个API
4. 输入股票代码，输出统一的股票数据格式

**技术需求**：
1. 创建自定义Credential类型，支持多个API Key
2. 创建自定义节点，支持API选择
3. 实现统一的输出格式转换
4. 处理不同API的错误响应

**输出格式统一**：
无论使用哪个API，输出格式都应该是：
```json
{
  "symbol": "AAPL",
  "name": "Apple Inc.",
  "price": 150.25,
  "change": 2.5,
  "changePercent": 1.69,
  "volume": 50000000,
  "marketCap": 2500000000000,
  "timestamp": "2024-01-15T10:30:00Z"
}
```

---

## 详细教程

### 第一步：准备开发环境

#### 1.1 克隆N8N仓库

首先，我们需要获取N8N的源代码，以便在其中添加自定义节点。

```bash
# 克隆N8N仓库
git clone https://github.com/n8n-io/n8n.git
cd n8n

# 安装依赖
npm install
```

#### 1.2 了解N8N项目结构

N8N的项目结构如下：

```
n8n/
├── nodes/              # 节点定义目录
│   ├── base/          # 基础节点
│   ├── n8n-nodes-base/ # 基础节点库
│   └── [YourNode]/    # 你的自定义节点（待创建）
├── credentials/        # Credential定义目录
│   └── [YourCredential]/ # 你的自定义Credential（待创建）
├── package.json        # 项目配置
└── tsconfig.json       # TypeScript配置
```

#### 1.3 创建开发分支

```bash
# 创建开发分支
git checkout -b custom-stock-node

# 确保在正确的目录
pwd  # 应该显示 n8n 目录路径
```

---

### 第二步：创建Credential类型

#### 2.1 理解Credential的作用

Credential用于存储和管理认证信息。在我们的案例中，需要支持多个API Key，所以我们需要创建一个能够存储多个API Key的Credential类型。

**设计思路**：
- 创建一个Credential类型：`StockApiCredential`
- 支持存储多个API的Key：
  - `alphaVantageApiKey`: Alpha Vantage的API Key
  - `finnhubApiKey`: Finnhub的API Key
  - `polygonApiKey`: Polygon.io的API Key

#### 2.2 创建Credential目录结构

```bash
# 在credentials目录下创建新目录
mkdir -p credentials/StockApiCredential
cd credentials/StockApiCredential
```

#### 2.3 创建Credential定义文件

创建文件 `StockApiCredential.credentials.ts`：

```typescript
import {
	ICredentialType,
	INodeProperties,
} from 'n8n-workflow';

export class StockApiCredential implements ICredentialType {
	name = 'stockApiCredential';
	displayName = 'Stock API Credential';
	documentationUrl = 'https://docs.n8n.io/integrations/stock-api';
	properties: INodeProperties[] = [
		{
			displayName: 'Alpha Vantage API Key',
			name: 'alphaVantageApiKey',
			type: 'string',
			typeOptions: {
				password: true,
			},
			default: '',
			description: 'API Key for Alpha Vantage. Get it from https://www.alphavantage.co/support/#api-key',
		},
		{
			displayName: 'Finnhub API Key',
			name: 'finnhubApiKey',
			type: 'string',
			typeOptions: {
				password: true,
			},
			default: '',
			description: 'API Key for Finnhub. Get it from https://finnhub.io/register',
		},
		{
			displayName: 'Polygon.io API Key',
			name: 'polygonApiKey',
			type: 'string',
			typeOptions: {
				password: true,
			},
			default: '',
			description: 'API Key for Polygon.io. Get it from https://polygon.io/dashboard/signup',
		},
	];
}
```

**代码说明**：
- `ICredentialType`: N8N的Credential类型接口
- `name`: Credential的内部标识符
- `displayName`: 在N8N界面中显示的名称
- `properties`: 定义Credential的属性（API Keys）
- `typeOptions.password: true`: 表示这是密码字段，输入时会隐藏

#### 2.4 注册Credential

在 `credentials/index.ts` 中注册新的Credential：

```typescript
import { StockApiCredential } from './StockApiCredential/StockApiCredential.credentials';

// 在导出列表中添加
export const credentialsTypes = {
	// ... 其他credentials
	stockApiCredential: StockApiCredential,
};
```

---

### 第三步：创建自定义节点

#### 3.1 创建节点目录结构

```bash
# 返回到n8n根目录
cd ../..

# 创建节点目录
mkdir -p nodes/StockData
cd nodes/StockData
```

#### 3.2 创建节点定义文件

创建文件 `StockData.node.json`：

```json
{
	"node": {
		"version": 1,
		"name": "stockData",
		"displayName": "Stock Data",
		"description": "Query stock data from multiple APIs (Alpha Vantage, Finnhub, Polygon.io)",
		"defaults": {
			"name": "Stock Data"
		},
		"inputs": ["main"],
		"outputs": ["main"],
		"credentials": [
			{
				"name": "stockApiCredential",
				"required": true
			}
		],
		"properties": [
			{
				"displayName": "API Provider",
				"name": "apiProvider",
				"type": "options",
				"options": [
					{
						"name": "Alpha Vantage",
						"value": "alphaVantage"
					},
					{
						"name": "Finnhub",
						"value": "finnhub"
					},
					{
						"name": "Polygon.io",
						"value": "polygon"
					}
				],
				"default": "alphaVantage",
				"required": true,
				"description": "Select the stock API provider to use"
			},
			{
				"displayName": "Stock Symbol",
				"name": "symbol",
				"type": "string",
				"default": "AAPL",
				"required": true,
				"description": "The stock symbol to query (e.g., AAPL, MSFT, GOOGL)"
			},
			{
				"displayName": "Additional Fields",
				"name": "additionalFields",
				"type": "collection",
				"placeholder": "Add Field",
				"default": {},
				"options": [
					{
						"displayName": "Output Size",
						"name": "outputSize",
						"type": "options",
						"options": [
							{
								"name": "Compact",
								"value": "compact"
							},
							{
								"name": "Full",
								"value": "full"
							}
						],
						"default": "compact",
						"description": "The size of the output data (only for Alpha Vantage)"
					}
				]
			}
		]
	}
}
```

**配置说明**：
- `name`: 节点的内部标识符
- `displayName`: 在N8N界面中显示的名称
- `credentials`: 指定节点使用的Credential类型
- `properties`: 定义节点的配置选项
  - `apiProvider`: 选择API提供商
  - `symbol`: 股票代码
  - `additionalFields`: 额外配置选项

#### 3.3 创建节点执行代码

创建文件 `StockData.ts`：

```typescript
import {
	IExecuteFunctions,
	INodeExecutionData,
	INodeType,
	INodeTypeDescription,
	NodePropertyTypes,
} from 'n8n-workflow';
import { IDataObject } from 'n8n-workflow';
import { OptionsWithUri } from 'request';

export class StockData implements INodeType {
	description: INodeTypeDescription = {
		displayName: 'Stock Data',
		name: 'stockData',
		icon: 'file:stock.svg',
		group: ['transform'],
		version: 1,
		subtitle: '={{$parameter["apiProvider"]}} - {{$parameter["symbol"]}}',
		description: 'Query stock data from multiple APIs',
		defaults: {
			name: 'Stock Data',
		},
		inputs: ['main'],
		outputs: ['main'],
		credentials: [
			{
				name: 'stockApiCredential',
				required: true,
			},
		],
		properties: [
			{
				displayName: 'API Provider',
				name: 'apiProvider',
				type: 'options',
				options: [
					{
						name: 'Alpha Vantage',
						value: 'alphaVantage',
					},
					{
						name: 'Finnhub',
						value: 'finnhub',
					},
					{
						name: 'Polygon.io',
						value: 'polygon',
					},
				],
				default: 'alphaVantage',
				required: true,
				description: 'Select the stock API provider to use',
			},
			{
				displayName: 'Stock Symbol',
				name: 'symbol',
				type: 'string',
				default: 'AAPL',
				required: true,
				description: 'The stock symbol to query (e.g., AAPL, MSFT, GOOGL)',
			},
			{
				displayName: 'Additional Fields',
				name: 'additionalFields',
				type: 'collection',
				placeholder: 'Add Field',
				default: {},
				options: [
					{
						displayName: 'Output Size',
						name: 'outputSize',
						type: 'options',
						options: [
							{
								name: 'Compact',
								value: 'compact',
							},
							{
								name: 'Full',
								value: 'full',
							},
						],
						default: 'compact',
						description: 'The size of the output data (only for Alpha Vantage)',
					},
				],
			},
		],
	};

	async execute(this: IExecuteFunctions): Promise<INodeExecutionData[][]> {
		const items = this.getInputData();
		const returnData: INodeExecutionData[] = [];

		for (let i = 0; i < items.length; i++) {
			try {
				const apiProvider = this.getNodeParameter('apiProvider', i) as string;
				const symbol = this.getNodeParameter('symbol', i) as string;
				const additionalFields = this.getNodeParameter('additionalFields', i) as IDataObject;

				// 获取Credential
				const credentials = await this.getCredentials('stockApiCredential');

				// 根据选择的API提供商调用不同的API
				let stockData: IDataObject;
				switch (apiProvider) {
					case 'alphaVantage':
						stockData = await this.callAlphaVantage(symbol, credentials, additionalFields);
						break;
					case 'finnhub':
						stockData = await this.callFinnhub(symbol, credentials);
						break;
					case 'polygon':
						stockData = await this.callPolygon(symbol, credentials);
						break;
					default:
						throw new Error(`Unsupported API provider: ${apiProvider}`);
				}

				// 统一输出格式
				const unifiedData = this.unifyOutputFormat(stockData, symbol, apiProvider);

				returnData.push({
					json: unifiedData,
					pairedItem: {
						item: i,
					},
				});
			} catch (error) {
				if (this.continueOnFail()) {
					returnData.push({
						json: {
							error: error.message,
						},
						pairedItem: {
							item: i,
						},
					});
					continue;
				}
				throw error;
			}
		}

		return [returnData];
	}

	/**
	 * 调用Alpha Vantage API
	 */
	private async callAlphaVantage(
		symbol: string,
		credentials: IDataObject,
		additionalFields: IDataObject,
	): Promise<IDataObject> {
		const apiKey = credentials.alphaVantageApiKey as string;
		if (!apiKey) {
			throw new Error('Alpha Vantage API Key is required');
		}

		const outputSize = (additionalFields.outputSize as string) || 'compact';

		const options: OptionsWithUri = {
			method: 'GET',
			uri: 'https://www.alphavantage.co/query',
			qs: {
				function: 'GLOBAL_QUOTE',
				symbol: symbol,
				apikey: apiKey,
			},
			json: true,
		};

		const response = await this.helpers.request(options);

		if (response['Error Message']) {
			throw new Error(`Alpha Vantage API Error: ${response['Error Message']}`);
		}

		if (response['Note']) {
			throw new Error(`Alpha Vantage API Rate Limit: ${response['Note']}`);
		}

		const quote = response['Global Quote'];
		if (!quote) {
			throw new Error('Invalid response from Alpha Vantage API');
		}

		return {
			symbol: quote['01. symbol'],
			price: parseFloat(quote['05. price']),
			change: parseFloat(quote['09. change']),
			changePercent: parseFloat(quote['10. change percent'].replace('%', '')),
			volume: parseInt(quote['06. volume'], 10),
			high: parseFloat(quote['03. high']),
			low: parseFloat(quote['04. low']),
			open: parseFloat(quote['02. open']),
			previousClose: parseFloat(quote['08. previous close']),
			timestamp: quote['07. latest trading day'],
			apiProvider: 'alphaVantage',
		};
	}

	/**
	 * 调用Finnhub API
	 */
	private async callFinnhub(symbol: string, credentials: IDataObject): Promise<IDataObject> {
		const apiKey = credentials.finnhubApiKey as string;
		if (!apiKey) {
			throw new Error('Finnhub API Key is required');
		}

		const options: OptionsWithUri = {
			method: 'GET',
			uri: 'https://finnhub.io/api/v1/quote',
			qs: {
				symbol: symbol,
				token: apiKey,
			},
			json: true,
		};

		const response = await this.helpers.request(options);

		if (response.error) {
			throw new Error(`Finnhub API Error: ${response.error}`);
		}

		// 获取公司信息
		const profileOptions: OptionsWithUri = {
			method: 'GET',
			uri: 'https://finnhub.io/api/v1/stock/profile2',
			qs: {
				symbol: symbol,
				token: apiKey,
			},
			json: true,
		};

		const profile = await this.helpers.request(profileOptions);

		return {
			symbol: symbol,
			price: response.c,
			change: response.d,
			changePercent: response.dp,
			volume: response.v,
			high: response.h,
			low: response.l,
			open: response.o,
			previousClose: response.pc,
			timestamp: new Date(response.t * 1000).toISOString(),
			name: profile.name || symbol,
			marketCap: profile.marketCapitalization || null,
			apiProvider: 'finnhub',
		};
	}

	/**
	 * 调用Polygon.io API
	 */
	private async callPolygon(symbol: string, credentials: IDataObject): Promise<IDataObject> {
		const apiKey = credentials.polygonApiKey as string;
		if (!apiKey) {
			throw new Error('Polygon.io API Key is required');
		}

		// 获取最新报价
		const options: OptionsWithUri = {
			method: 'GET',
			uri: `https://api.polygon.io/v2/aggs/ticker/${symbol}/prev`,
			qs: {
				adjusted: 'true',
				apikey: apiKey,
			},
			json: true,
		};

		const response = await this.helpers.request(options);

		if (response.status !== 'OK') {
			throw new Error(`Polygon.io API Error: ${response.status}`);
		}

		if (!response.results || response.results.length === 0) {
			throw new Error('No data returned from Polygon.io API');
		}

		const result = response.results[0];
		const previousClose = result.c; // 收盘价作为当前价格（因为prev是前一个交易日）

		// 获取实时报价（如果可用）
		let currentPrice = previousClose;
		try {
			const snapshotOptions: OptionsWithUri = {
				method: 'GET',
				uri: `https://api.polygon.io/v2/snapshot/locale/us/markets/stocks/tickers/${symbol}`,
				qs: {
					apikey: apiKey,
				},
				json: true,
			};

			const snapshot = await this.helpers.request(snapshotOptions);
			if (snapshot.ticker && snapshot.ticker.day) {
				currentPrice = snapshot.ticker.day.c; // 当前收盘价
			}
		} catch (error) {
			// 如果实时报价失败，使用前一个交易日的收盘价
			console.warn('Failed to get real-time quote, using previous close');
		}

		const change = currentPrice - previousClose;
		const changePercent = (change / previousClose) * 100;

		return {
			symbol: symbol,
			price: currentPrice,
			change: change,
			changePercent: changePercent,
			volume: result.v,
			high: result.h,
			low: result.l,
			open: result.o,
			previousClose: previousClose,
			timestamp: new Date(result.t).toISOString(),
			apiProvider: 'polygon',
		};
	}

	/**
	 * 统一输出格式
	 */
	private unifyOutputFormat(
		data: IDataObject,
		symbol: string,
		apiProvider: string,
	): IDataObject {
		return {
			symbol: data.symbol || symbol,
			name: data.name || symbol,
			price: data.price || 0,
			change: data.change || 0,
			changePercent: data.changePercent || 0,
			volume: data.volume || 0,
			high: data.high || null,
			low: data.low || null,
			open: data.open || null,
			previousClose: data.previousClose || null,
			marketCap: data.marketCap || null,
			timestamp: data.timestamp || new Date().toISOString(),
			apiProvider: apiProvider,
			rawData: data, // 保留原始数据以便调试
		};
	}
}
```

**代码说明**：
- `execute`: 节点的主要执行函数
- `callAlphaVantage`, `callFinnhub`, `callPolygon`: 调用不同API的方法
- `unifyOutputFormat`: 统一输出格式的方法
- `this.helpers.request`: N8N提供的HTTP请求辅助方法
- `this.getCredentials`: 获取Credential的方法
- `this.getNodeParameter`: 获取节点参数的方法

#### 3.4 注册节点

在 `nodes/index.ts` 中注册新节点：

```typescript
import { StockData } from './StockData/StockData';

// 在导出列表中添加
export const nodes = [
	// ... 其他节点
	StockData,
];
```

---

### 第四步：编译和测试

#### 4.1 编译TypeScript代码

```bash
# 返回到n8n根目录
cd ../..

# 编译TypeScript
npm run build
```

#### 4.2 启动N8N开发服务器

```bash
# 启动开发服务器
npm run dev
```

#### 4.3 在N8N中测试节点

1. 打开浏览器访问 `http://localhost:5678`
2. 创建新工作流
3. 在节点列表中找到 "Stock Data" 节点
4. 添加节点到工作流
5. 配置Credential：
   - 点击 "Credentials" 下拉菜单
   - 选择 "Create New Credential"
   - 选择 "Stock API Credential"
   - 输入至少一个API Key（Alpha Vantage、Finnhub或Polygon.io）
6. 配置节点：
   - 选择API Provider
   - 输入Stock Symbol（如：AAPL）
7. 执行工作流并查看结果

---

### 第五步：优化和增强

#### 5.1 添加错误处理

在节点代码中添加更完善的错误处理：

```typescript
private async callAlphaVantage(
	symbol: string,
	credentials: IDataObject,
	additionalFields: IDataObject,
): Promise<IDataObject> {
	const apiKey = credentials.alphaVantageApiKey as string;
	if (!apiKey) {
		throw new Error('Alpha Vantage API Key is required. Please configure it in credentials.');
	}

	try {
		const options: OptionsWithUri = {
			method: 'GET',
			uri: 'https://www.alphavantage.co/query',
			qs: {
				function: 'GLOBAL_QUOTE',
				symbol: symbol,
				apikey: apiKey,
			},
			json: true,
			timeout: 10000, // 10秒超时
		};

		const response = await this.helpers.request(options);

		// 处理API错误响应
		if (response['Error Message']) {
			throw new Error(`Alpha Vantage API Error: ${response['Error Message']}`);
		}

		if (response['Note']) {
			throw new Error(`Alpha Vantage API Rate Limit: ${response['Note']}. Please wait a moment and try again.`);
		}

		// 验证响应数据
		const quote = response['Global Quote'];
		if (!quote || !quote['05. price']) {
			throw new Error('Invalid response from Alpha Vantage API. The stock symbol may not exist.');
		}

		// ... 其余代码
	} catch (error) {
		if (error.code === 'ETIMEDOUT') {
			throw new Error('Request to Alpha Vantage API timed out. Please try again.');
		}
		if (error.code === 'ENOTFOUND') {
			throw new Error('Cannot connect to Alpha Vantage API. Please check your internet connection.');
		}
		throw error;
	}
}
```

#### 5.2 添加缓存机制

为了避免频繁调用API，可以添加简单的缓存机制：

```typescript
// 在类中添加缓存属性
private cache: Map<string, { data: IDataObject; timestamp: number }> = new Map();
private readonly CACHE_TTL = 60000; // 缓存1分钟

private getCachedData(key: string): IDataObject | null {
	const cached = this.cache.get(key);
	if (cached && Date.now() - cached.timestamp < this.CACHE_TTL) {
		return cached.data;
	}
	return null;
}

private setCachedData(key: string, data: IDataObject): void {
	this.cache.set(key, {
		data,
		timestamp: Date.now(),
	});
}
```

#### 5.3 添加日志记录

```typescript
// 在执行方法中添加日志
async execute(this: IExecuteFunctions): Promise<INodeExecutionData[][]> {
	const items = this.getInputData();
	const returnData: INodeExecutionData[] = [];

	for (let i = 0; i < items.length; i++) {
		try {
			const apiProvider = this.getNodeParameter('apiProvider', i) as string;
			const symbol = this.getNodeParameter('symbol', i) as string;

			// 记录日志
			this.logger.info(`Querying stock data for ${symbol} using ${apiProvider}`);

			// ... 执行逻辑

			this.logger.info(`Successfully retrieved data for ${symbol}`);
		} catch (error) {
			this.logger.error(`Error querying stock data: ${error.message}`);
			// ... 错误处理
		}
	}

	return [returnData];
}
```

---

## 实践练习

### 练习1：创建基础节点

**任务目标**：创建一个最简单的自定义节点，输出固定的JSON数据。

**前置条件**：
- 已安装Node.js和npm
- 已克隆N8N仓库
- 已安装依赖

**详细步骤**：

1. **创建节点目录**
   ```bash
   mkdir -p nodes/HelloWorld
   cd nodes/HelloWorld
   ```

2. **创建节点定义文件** `HelloWorld.node.json`
   ```json
   {
     "node": {
       "version": 1,
       "name": "helloWorld",
       "displayName": "Hello World",
       "description": "A simple hello world node",
       "defaults": {
         "name": "Hello World"
       },
       "inputs": ["main"],
       "outputs": ["main"],
       "properties": []
     }
   }
   ```

3. **创建节点代码文件** `HelloWorld.ts`
   ```typescript
   import {
     IExecuteFunctions,
     INodeExecutionData,
     INodeType,
     INodeTypeDescription,
   } from 'n8n-workflow';

   export class HelloWorld implements INodeType {
     description: INodeTypeDescription = {
       displayName: 'Hello World',
       name: 'helloWorld',
       icon: 'file:hello.svg',
       group: ['transform'],
       version: 1,
       description: 'A simple hello world node',
       defaults: {
         name: 'Hello World',
       },
       inputs: ['main'],
       outputs: ['main'],
       properties: [],
     };

     async execute(this: IExecuteFunctions): Promise<INodeExecutionData[][]> {
       const returnData: INodeExecutionData[] = [{
         json: {
           message: 'Hello World from N8N!',
           timestamp: new Date().toISOString(),
         },
       }];

       return [returnData];
     }
   }
   ```

4. **注册节点**（在 `nodes/index.ts` 中）
5. **编译并测试**

**预期结果**：节点能够成功执行，输出包含 "Hello World from N8N!" 的消息。

**验证方法**：
- 在N8N中创建新工作流
- 添加Hello World节点
- 执行工作流
- 检查输出数据

---

### 练习2：添加Credential支持

**任务目标**：为Hello World节点添加Credential支持，从Credential中读取配置。

**详细步骤**：

1. **创建Credential类型** `HelloWorldCredential.credentials.ts`
2. **定义Credential属性**（如：用户名、密码）
3. **在节点中使用Credential**
4. **测试Credential配置**

**预期结果**：节点能够从Credential中读取配置并使用。

---

### 练习3：完善股票数据节点

**任务目标**：基于本教程的案例，完善股票数据节点，添加以下功能：

1. **支持批量查询**：一次查询多个股票
2. **添加数据验证**：验证股票代码格式
3. **添加重试机制**：API调用失败时自动重试
4. **优化输出格式**：添加更多字段（如：52周最高/最低价）

**详细步骤**：

1. **修改节点属性**，添加批量查询选项
2. **实现批量查询逻辑**
3. **添加数据验证函数**
4. **实现重试机制**
5. **扩展输出格式**

**预期结果**：节点能够批量查询股票数据，具备完善的错误处理和重试机制。

---

## 常见问题

### Q1: 编译时出现TypeScript错误怎么办？

**A**: 常见的TypeScript错误及解决方法：

1. **类型错误**：确保所有类型都正确定义
   ```typescript
   // 错误
   const apiKey = credentials.apiKey;
   
   // 正确
   const apiKey = credentials.apiKey as string;
   ```

2. **导入错误**：确保导入路径正确
   ```typescript
   // 确保从正确的包导入
   import { IExecuteFunctions } from 'n8n-workflow';
   ```

3. **属性不存在**：检查N8N版本，某些属性可能在不同版本中不同

### Q2: 节点在N8N中不显示怎么办？

**A**: 检查以下几点：

1. **节点是否已注册**：检查 `nodes/index.ts` 中的导出
2. **编译是否成功**：运行 `npm run build` 检查是否有错误
3. **重启N8N**：修改节点后需要重启N8N
4. **清除缓存**：删除 `.n8n` 目录并重新启动

### Q3: Credential无法保存怎么办？

**A**: 可能的原因：

1. **Credential未注册**：检查 `credentials/index.ts`
2. **属性定义错误**：检查Credential属性定义
3. **类型不匹配**：确保属性类型正确

### Q4: API调用失败怎么办？

**A**: 调试步骤：

1. **检查API Key**：确保API Key正确且有效
2. **检查网络连接**：确保能够访问API端点
3. **查看错误信息**：检查N8N执行日志
4. **测试API**：使用curl或Postman直接测试API
5. **检查频率限制**：某些API有请求频率限制

### Q5: 如何调试自定义节点？

**A**: 调试方法：

1. **使用console.log**：在代码中添加日志
2. **使用N8N日志**：使用 `this.logger` 记录日志
3. **检查执行历史**：在N8N中查看节点执行历史
4. **使用调试器**：在VS Code中设置断点调试

### Q6: 如何发布自定义节点？

**A**: 发布步骤：

1. **创建npm包**：将节点打包为npm包
2. **发布到npm**：使用 `npm publish`
3. **创建文档**：编写使用文档
4. **提交到N8N社区**：可以提交到N8N社区节点列表

### Q7: 如何处理不同API的响应格式差异？

**A**: 最佳实践：

1. **统一输出格式**：创建统一的数据结构
2. **数据转换函数**：为每个API创建转换函数
3. **错误处理**：处理不同API的错误格式
4. **数据验证**：验证转换后的数据完整性

### Q8: 如何优化节点性能？

**A**: 优化建议：

1. **添加缓存**：避免重复API调用
2. **批量处理**：一次处理多个项目
3. **异步处理**：使用Promise.all并行处理
4. **减少API调用**：合并多个API调用为一个

---

## 知识检查

### 选择题

1. **自定义节点的定义文件是什么格式？**
   - A. JSON
   - B. TypeScript
   - C. JavaScript
   - D. YAML
   - **答案**：A（节点定义是JSON格式，执行代码是TypeScript）

2. **Credential的作用是什么？**
   - A. 存储节点配置
   - B. 存储认证信息
   - C. 存储工作流数据
   - D. 存储用户信息
   - **答案**：B

3. **如何获取节点参数？**
   - A. `this.getParameter()`
   - B. `this.getNodeParameter()`
   - C. `this.getConfig()`
   - D. `this.getSettings()`
   - **答案**：B

4. **如何获取Credential？**
   - A. `this.getCredentials()`
   - B. `this.getAuth()`
   - C. `this.getCredential()`
   - D. `this.getToken()`
   - **答案**：A

5. **节点的执行函数返回什么类型？**
   - A. `Promise<INodeExecutionData>`
   - B. `Promise<INodeExecutionData[]>`
   - C. `Promise<INodeExecutionData[][]>`
   - D. `Promise<void>`
   - **答案**：C（返回二维数组，因为可能有多个输出）

### 实践题

1. **创建一个简单的HTTP请求节点**
   - 要求：能够发送GET请求到指定URL
   - 输入：URL
   - 输出：响应数据

2. **为节点添加条件判断**
   - 要求：根据输入数据的不同值执行不同逻辑
   - 使用IF节点或Switch节点的逻辑

3. **实现数据转换节点**
   - 要求：将输入数据转换为指定格式
   - 支持多种转换规则

---

## 延伸阅读

### 官方资源

1. **N8N节点开发文档**
   - 网址：https://docs.n8n.io/integrations/creating-nodes/
   - 内容：官方节点开发指南

2. **N8N GitHub仓库**
   - 网址：https://github.com/n8n-io/n8n
   - 内容：源代码和示例节点

3. **N8N社区节点**
   - 网址：https://github.com/n8n-io/n8n-nodes
   - 内容：社区贡献的节点

### 学习资源

1. **TypeScript官方文档**
   - 网址：https://www.typescriptlang.org/docs/
   - 内容：TypeScript语言参考

2. **Node.js官方文档**
   - 网址：https://nodejs.org/docs/
   - 内容：Node.js API参考

3. **N8N社区论坛**
   - 网址：https://community.n8n.io/
   - 内容：社区讨论和问题解答

### 相关教程

1. **N8N工作流开发最佳实践**
2. **API集成模式**
3. **错误处理策略**
4. **性能优化技巧**

---

## 快速参考

### 节点开发检查清单

- [ ] 创建节点目录结构
- [ ] 定义节点JSON文件
- [ ] 实现节点TypeScript代码
- [ ] 注册节点
- [ ] 创建Credential（如需要）
- [ ] 注册Credential（如需要）
- [ ] 编译代码
- [ ] 测试节点功能
- [ ] 添加错误处理
- [ ] 编写文档

### 常用代码片段

**获取节点参数**：
```typescript
const param = this.getNodeParameter('paramName', 0) as string;
```

**获取Credential**：
```typescript
const credentials = await this.getCredentials('credentialName');
```

**发送HTTP请求**：
```typescript
const response = await this.helpers.request({
  method: 'GET',
  uri: 'https://api.example.com',
  json: true,
});
```

**返回数据**：
```typescript
return [[{
  json: { data: 'value' },
  pairedItem: { item: 0 },
}]];
```

---

## 下一步学习

完成本教程后，你可以：

1. **扩展股票数据节点**：添加更多API支持、添加历史数据查询等
2. **创建其他自定义节点**：根据你的业务需求创建节点
3. **学习高级特性**：学习节点的高级特性，如动态参数、条件输出等
4. **参与社区贡献**：将你的节点贡献给N8N社区

**祝开发顺利！** 🚀

