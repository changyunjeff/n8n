# Chapter 2: How to Install and Configure N8N from Scratch?

## Problem Introduction

You've learned what N8N is and how it solves practical problems. Now, you're probably eager to start using N8N and create your first automated workflow. However, as a technical beginner, you might encounter your first challenge: how to install N8N?

You might be thinking: "What do I need to install on my computer? Do I need programming knowledge? Will it be complicated?" These concerns are normal. The good news is that N8N provides multiple installation methods, from the simplest quick start to professional cloud deployment, and there's always a method suitable for your technical level and needs.

This chapter will teach you step-by-step how to install and configure N8N from scratch. Whether you're a complete technical beginner or an experienced developer, you can find an installation method that suits you. We'll start with the simplest npx quick start, then gradually introduce Docker installation, npm global installation, and cloud platform deployment. We'll also explain in detail how to perform initial configuration, familiarize yourself with N8N's interface, and solve common installation problems.

## Core Concepts

### Overview of N8N Installation Methods

N8N provides multiple installation methods, each with its applicable scenarios and pros/cons. Understanding the differences between these installation methods can help you choose the one that best suits you.

#### Installation Method Comparison Table

| Installation Method | Use Cases | Advantages | Disadvantages | Technical Difficulty |
|---------------------|-----------|------------|---------------|---------------------|
| **npx Quick Start** | Local testing, learning, quick experience | No installation needed, simple and fast, suitable for beginners | Data not persistent, lost after restart | ⭐ Very Simple |
| **npm Global Installation** | Long-term use, local development | Stable, data persistent, easy to manage | Requires Node.js environment | ⭐⭐ Simple |
| **Docker Installation** | Have Docker environment, need isolation | Good isolation, easy to manage, portable | Requires Docker knowledge | ⭐⭐⭐ Medium |
| **Cloud Platform Deployment** | Production environment, team use | High availability, easy to scale, professional support | Requires payment, needs configuration | ⭐⭐⭐⭐ Complex |

#### Selection Recommendations

**If you're a technical beginner**:
- **Recommendation**: npx quick start
- **Reason**: Simplest, no installation needed, can quickly experience N8N's features

**If you're a personal user wanting long-term use**:
- **Recommendation**: npm global installation or Docker installation
- **Reason**: Data persistence, can use long-term, relatively simple configuration

**If you're using for a team or need production environment**:
- **Recommendation**: Cloud platform deployment or Docker Compose
- **Reason**: High availability, easy to maintain, supports multiple users

### System Requirements

Before starting installation, understanding N8N's system requirements is important:

#### Minimum System Requirements

| Resource | Minimum Requirement | Recommended Configuration |
|----------|---------------------|---------------------------|
| **CPU** | 1 core | 2 cores or more |
| **Memory** | 1GB RAM | 2GB RAM or more |
| **Storage** | 1GB available space | 10GB or more |
| **Operating System** | Windows 10+, macOS 10.14+, Linux | Latest version |

#### Software Dependencies

Different installation methods require different software dependencies:

- **npx method**: Requires Node.js (will download automatically, but recommended to pre-install)
- **npm method**: Requires Node.js 16.0 or higher
- **Docker method**: Requires Docker and Docker Compose
- **Cloud platform method**: Requires corresponding cloud platform account and basic configuration knowledge

### Environment Variables and Configuration

N8N uses environment variables to configure various settings. Understanding these environment variables can help you better configure N8N.

#### Common Environment Variables

| Environment Variable | Description | Default Value | Example |
|---------------------|-------------|---------------|---------|
| `N8N_PORT` | Port N8N runs on | 5678 | `N8N_PORT=5678` |
| `N8N_HOST` | Host N8N binds to | localhost | `N8N_HOST=0.0.0.0` |
| `N8N_PROTOCOL` | Protocol type | http | `N8N_PROTOCOL=https` |
| `N8N_BASIC_AUTH_ACTIVE` | Enable basic authentication | false | `N8N_BASIC_AUTH_ACTIVE=true` |
| `N8N_BASIC_AUTH_USER` | Basic auth username | - | `N8N_BASIC_AUTH_USER=admin` |
| `N8N_BASIC_AUTH_PASSWORD` | Basic auth password | - | `N8N_BASIC_AUTH_PASSWORD=password` |
| `N8N_ENCRYPTION_KEY` | Encryption key | - | `N8N_ENCRYPTION_KEY=your-key` |

## Detailed Tutorial

### Step 1: Preparation

Before starting installation, we need to do some preparation work.

#### 1.1 Check System Requirements

**Windows System**:
1. Open "Settings" → "System" → "About"
2. Check Windows version (requires Windows 10 or higher)
3. Check system type (32-bit or 64-bit)

**macOS System**:
1. Click Apple menu → "About This Mac"
2. Check macOS version (requires macOS 10.14 or higher)

**Linux System**:
```bash
# Check system information
uname -a
# Check available memory
free -h
# Check disk space
df -h
```

#### 1.2 Install Node.js (if needed)

If you choose npm or npx installation method, you need to install Node.js first.

**Check if Node.js is installed**:
```bash
node --version
npm --version
```

**If not installed, download and install Node.js**:
1. Visit Node.js website: https://nodejs.org
2. Download LTS (Long Term Support) version
3. Run the installer and follow the prompts to complete installation
4. Verify installation:
```bash
node --version  # Should show version, e.g., v18.17.0
npm --version   # Should show version, e.g., 9.6.7
```

**Notes**:
- Recommended to install LTS version (Long Term Support version)
- Ensure Node.js version is 16.0 or higher
- May need to restart terminal after installation

#### 1.3 Install Docker (if needed)

If you choose Docker installation method, you need to install Docker first.

**Windows/macOS**:
1. Download Docker Desktop: https://www.docker.com/products/docker-desktop
2. Run the installer
3. Start Docker Desktop
4. Verify installation:
```bash
docker --version
docker-compose --version
```

**Linux**:
```bash
# Ubuntu/Debian
sudo apt-get update
sudo apt-get install docker.io docker-compose

# Verify installation
docker --version
docker-compose --version
```

### Step 2: Method A - Using npx Quick Start (Recommended for Beginners)

This is the simplest installation method, suitable for quickly experiencing N8N's features.

#### 2.1 Start N8N

**Windows PowerShell**:
```powershell
npx n8n
```

**macOS/Linux Terminal**:
```bash
npx n8n
```

**Explanation**:
- First run will download N8N (may take a few minutes)
- Will automatically start N8N after download completes
- Default access address: http://localhost:5678

#### 2.2 Access N8N Interface

1. Open browser
2. Visit: http://localhost:5678
3. You'll see N8N's welcome interface

[Screenshot location: N8N welcome interface]

#### 2.3 Create Administrator Account

1. On the welcome interface, click "Get started"
2. Fill in administrator information:
   - **Email**: Your email address
   - **First Name**: First name
   - **Last Name**: Last name
   - **Password**: Set password (at least 8 characters)
3. Click "Create account"
4. After login, enter N8N main interface

[Screenshot location: Create account interface]

#### 2.4 Notes

**Important Notes**:
- ⚠️ npx method data is not persistently saved, data will be lost after closing terminal
- ⚠️ This method is only suitable for testing and learning, not for production use
- ⚠️ Need to recreate account each time you start (unless using environment variables to save data)

**Method to Save Data**:
If you want to save data in npx method, you can set data directory:
```bash
# Windows PowerShell
$env:N8N_USER_FOLDER="D:\n8n-data"
npx n8n

# macOS/Linux
export N8N_USER_FOLDER="$HOME/n8n-data"
npx n8n
```

### Step 3: Method B - Using npm Global Installation

This method is suitable for personal users who want to use N8N long-term.

#### 3.1 Globally Install N8N

```bash
npm install -g n8n
```

**Explanation**:
- `-g` parameter means global installation
- Installation process may take a few minutes
- After installation, you can run `n8n` command from anywhere

#### 3.2 Start N8N

```bash
n8n
```

**Explanation**:
- Default access address: http://localhost:5678
- Data will be saved in `.n8n` folder in user directory
- N8N will stop running after closing terminal

#### 3.3 Configure N8N (Optional)

You can configure N8N through environment variables:

**Windows PowerShell**:
```powershell
# Set port
$env:N8N_PORT=8080
# Set data directory
$env:N8N_USER_FOLDER="D:\n8n-data"
# Start N8N
npx n8n
```

**macOS/Linux**:
```bash
# Set port
export N8N_PORT=8080
# Set data directory
export N8N_USER_FOLDER="$HOME/n8n-data"
# Start N8N
n8n
```

#### 3.4 Set as System Service (Optional, Advanced)

If you want N8N to run in the background, you can set it as a system service. The specific method depends on your operating system, and we won't go into detail here.

### Step 4: Method C - Using Docker Installation

This method is suitable for users with Docker experience, providing better isolation and portability.

#### 4.1 Run N8N with Docker

**Basic Command**:
```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

**Command Explanation**:
- `-it`: Interactive terminal
- `--rm`: Automatically delete container after stopping
- `--name n8n`: Container name
- `-p 5678:5678`: Port mapping (host port:container port)
- `-v ~/.n8n:/home/node/.n8n`: Volume mount (save data)
- `n8nio/n8n`: N8N Docker image

#### 4.2 Using Docker Compose (Recommended)

Create `docker-compose.yml` file:

```yaml
version: '3.8'

services:
  n8n:
    image: n8nio/n8n
    container_name: n8n
    restart: always
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=your-password
    volumes:
      - ~/.n8n:/home/node/.n8n
```

**Start Service**:
```bash
docker-compose up -d
```

**Stop Service**:
```bash
docker-compose down
```

**View Logs**:
```bash
docker-compose logs -f
```

#### 4.3 Access N8N

1. Open browser
2. Visit: http://localhost:5678
3. If basic authentication is set, enter username and password

### Step 5: Method D - Cloud Platform Deployment (Overview)

Cloud platform deployment is suitable for production environments and team use. Here's a brief overview of several major cloud platforms.

#### 5.1 DigitalOcean Deployment

1. Create DigitalOcean account
2. Create Droplet (choose Ubuntu system)
3. Connect to Droplet
4. Install Docker and Docker Compose
5. Deploy N8N using Docker Compose
6. Configure domain and SSL certificate

#### 5.2 AWS Deployment

1. Create AWS account
2. Launch EC2 instance
3. Configure security group (open port 5678)
4. Connect to instance
5. Install Docker and deploy N8N
6. Configure Elastic IP and domain

#### 5.3 Other Cloud Platforms

- **Google Cloud Platform (GCP)**
- **Microsoft Azure**
- **Heroku**
- **Railway**
- **Render**

Each platform has different specific deployment steps. It's recommended to refer to N8N official documentation or the corresponding cloud platform's documentation.

### Step 6: Initial Configuration

Regardless of which installation method you use, you need to perform initial configuration after installation.

#### 6.1 Create Administrator Account

If you use npx method, you'll be prompted to create an account on first access. If you use other methods, you also need to create an administrator account.

**Configuration Steps**:
1. Access N8N interface (usually http://localhost:5678)
2. Fill in administrator information
3. Create account and login

#### 6.2 Configure Environment Variables

**Windows PowerShell**:
```powershell
# Set port
$env:N8N_PORT=8080

# Set host (allow external access)
$env:N8N_HOST=0.0.0.0

# Enable basic authentication
$env:N8N_BASIC_AUTH_ACTIVE=true
$env:N8N_BASIC_AUTH_USER=admin
$env:N8N_BASIC_AUTH_PASSWORD=your-secure-password

# Set data directory
$env:N8N_USER_FOLDER="D:\n8n-data"
```

**macOS/Linux**:
```bash
# Set port
export N8N_PORT=8080

# Set host
export N8N_HOST=0.0.0.0

# Enable basic authentication
export N8N_BASIC_AUTH_ACTIVE=true
export N8N_BASIC_AUTH_USER=admin
export N8N_BASIC_AUTH_PASSWORD=your-secure-password

# Set data directory
export N8N_USER_FOLDER="$HOME/n8n-data"
```

**Docker Method** (in docker-compose.yml):
```yaml
environment:
  - N8N_PORT=8080
  - N8N_HOST=0.0.0.0
  - N8N_BASIC_AUTH_ACTIVE=true
  - N8N_BASIC_AUTH_USER=admin
  - N8N_BASIC_AUTH_PASSWORD=your-secure-password
```

#### 6.3 Configure Webhook URL (if needed)

If you need to use Webhook triggers, you need to configure Webhook URL.

**Local Development**:
- Webhook URL format: `http://localhost:5678/webhook/your-workflow-id`

**Production Environment**:
- Need to configure domain and SSL certificate
- Webhook URL format: `https://your-domain.com/webhook/your-workflow-id`

**Configuration Steps**:
1. Configure `N8N_PROTOCOL=https` in N8N settings
2. Configure `N8N_WEBHOOK_URL=https://your-domain.com`
3. Ensure domain points to your server
4. Configure SSL certificate (can use Let's Encrypt)

### Step 7: Familiarize with N8N Interface

After completing installation and configuration, let's familiarize ourselves with N8N's user interface.

#### 7.1 Main Interface Layout

[Screenshot location: N8N main interface]

**Main Areas**:

1. **Left Sidebar**
   - **Workflows**: Workflow list
   - **Executions**: Execution history
   - **Templates**: Workflow templates
   - **Credentials**: Credential management
   - **Settings**: Settings

2. **Central Canvas**
   - Workflow design area
   - Drag and drop nodes to create connections
   - Visual workflow design

3. **Right Panel**
   - Node configuration panel
   - Set node parameters
   - View node documentation

4. **Top Toolbar**
   - **Save**: Save workflow
   - **Execute Workflow**: Execute workflow
   - **Test workflow**: Test workflow
   - **Settings**: Workflow settings

#### 7.2 Interface Navigation Challenge

Complete the following challenges to familiarize yourself with N8N interface:

**Challenge 1: Find Workflow List**
- Goal: Find workflow list within 30 seconds
- Location: "Workflows" in left sidebar

**Challenge 2: Find Execution History**
- Goal: Find execution history within 30 seconds
- Location: "Executions" in left sidebar

**Challenge 3: Find Template Library**
- Goal: Find template library within 30 seconds
- Location: "Templates" in left sidebar

**Challenge 4: Find Credential Management**
- Goal: Find credential management within 30 seconds
- Location: "Credentials" in left sidebar

**Challenge 5: Find Settings**
- Goal: Find settings within 30 seconds
- Location: "Settings" in left sidebar

#### 7.3 Draw Interface Functional Area Map

Create a simple interface map, labeling each functional area:

```
┌─────────────────────────────────────────────────┐
│  Top Toolbar: Save, Execute, Test, Settings    │
├──────────┬──────────────────────────┬───────────┤
│          │                          │           │
│  Left    │      Canvas              │  Right    │
│  Sidebar │      (Workflow Design)   │  Panel    │
│          │                          │  (Node    │
│  - Workflows                        │   Config) │
│  - Executions                       │           │
│  - Templates                        │           │
│  - Credentials                      │           │
│  - Settings                         │           │
│          │                          │           │
└──────────┴──────────────────────────┴───────────┘
```

## Practice Exercises

### Exercise 1: Installation Practice

**Task Objective**: Choose an installation method and successfully install and start N8N

**Prerequisites**:
- Prepare corresponding software environment based on chosen installation method
- Ensure stable network connection

**Detailed Steps**:

#### Method A: npx Quick Start (Recommended for Beginners)

1. **Check Node.js**
   ```bash
   node --version
   ```
   If not installed, visit https://nodejs.org to download and install

2. **Start N8N**
   ```bash
   npx n8n
   ```

3. **Wait for Download and Start**
   - First run will download N8N (may take a few minutes)
   - "Editor is now accessible via:" prompt indicates successful start

4. **Access N8N**
   - Open browser
   - Visit http://localhost:5678

5. **Create Account**
   - Fill in administrator information
   - Create account and login

**Expected Results**:
- N8N successfully started
- Can access N8N interface
- Successfully created administrator account

**Verification Method**:
- Check if browser can access http://localhost:5678
- Check if can successfully login to N8N

#### Method B: npm Global Installation

1. **Install Node.js** (if not installed)
   - Visit https://nodejs.org
   - Download and install LTS version

2. **Globally Install N8N**
   ```bash
   npm install -g n8n
   ```

3. **Start N8N**
   ```bash
   n8n
   ```

4. **Access and Configure**
   - Visit http://localhost:5678
   - Create administrator account

**Expected Results**:
- N8N successfully installed
- Can start via `n8n` command
- Data saved in user directory

**Verification Method**:
- Check if `n8n --version` command is available
- Check if data directory exists

#### Method C: Docker Installation

1. **Install Docker** (if not installed)
   - Visit https://www.docker.com/products/docker-desktop
   - Download and install Docker Desktop

2. **Create docker-compose.yml**
   ```yaml
   version: '3.8'
   services:
     n8n:
       image: n8nio/n8n
       container_name: n8n
       restart: always
       ports:
         - "5678:5678"
       volumes:
         - ~/.n8n:/home/node/.n8n
   ```

3. **Start Service**
   ```bash
   docker-compose up -d
   ```

4. **Access N8N**
   - Visit http://localhost:5678
   - Create administrator account

**Expected Results**:
- Docker container successfully running
- Can access N8N interface
- Data persistently saved

**Verification Method**:
- Check if `docker ps` shows n8n container running
- Check if data volume is correctly mounted

**Extended Challenge**:
- Configure basic authentication
- Set custom port
- Configure SSL certificate

**Troubleshooting**:
- **Problem**: npx command not found
  - **Solution**: Install Node.js, ensure npm is available
- **Problem**: Port 5678 is occupied
  - **Solution**: Use `N8N_PORT` environment variable to change port
- **Problem**: Docker container cannot start
  - **Solution**: Check if Docker is running, view container logs

### Exercise 2: Configuration Practice

**Task Objective**: Complete N8N's basic configuration, including account setup, environment variable configuration, etc.

**Prerequisites**:
- Completed Exercise 1, N8N successfully installed

**Detailed Steps**:

1. **Create Administrator Account**
   - Access N8N interface
   - Fill in administrator information (Email, name, password)
   - Create account and login

2. **Configure Environment Variables**
   - Set environment variables based on your installation method
   - Configure at least the following variables:
     - `N8N_PORT`: Set port (e.g., 8080)
     - `N8N_USER_FOLDER`: Set data directory

3. **Configure Basic Authentication** (Optional but recommended)
   - Set `N8N_BASIC_AUTH_ACTIVE=true`
   - Set username and password
   - Restart N8N
   - Verify that username and password are required to access

4. **Configure Workflow Storage Location**
   - Check data directory location
   - Confirm workflow data save location
   - Backup data directory (optional)

5. **Test Configuration**
   - Restart N8N
   - Verify all configurations are effective
   - Check if data is persistent

**Expected Results**:
- Administrator account successfully created
- Environment variables correctly configured
- Basic authentication effective (if configured)
- Data persistently saved

**Verification Method**:
- Check if can access N8N using configured port
- Check if files are generated in data directory
- Check if basic authentication is effective

**Extended Challenge**:
- Configure Webhook URL
- Configure SSL certificate
- Set multiple environment variables

**Troubleshooting**:
- **Problem**: Environment variables not effective
  - **Solution**: Check environment variable setting method, ensure set before starting
- **Problem**: Basic authentication not working
  - **Solution**: Check if environment variables are correctly set, restart N8N

### Exercise 3: Interface Exploration

**Task Objective**: Familiarize yourself with N8N's user interface and complete interface navigation challenges

**Prerequisites**:
- Completed Exercises 1 and 2, N8N installed and configured

**Detailed Steps**:

1. **Draw Interface Functional Area Map**
   - Open N8N interface
   - Observe each functional area
   - Draw simple interface map
   - Label each area's function

2. **Complete Interface Navigation Challenges**
   - **Challenge 1**: Find workflow list within 30 seconds
   - **Challenge 2**: Find execution history within 30 seconds
   - **Challenge 3**: Find template library within 30 seconds
   - **Challenge 4**: Find credential management within 30 seconds
   - **Challenge 5**: Find settings within 30 seconds

3. **Explore Each Functional Area**
   - Click "Workflows" to view workflow list
   - Click "Executions" to view execution history
   - Click "Templates" to browse workflow templates
   - Click "Credentials" to view credential management
   - Click "Settings" to view settings options

4. **Create First Workflow** (Simple test)
   - Click "Add workflow"
   - Add a node on workflow canvas
   - Save workflow
   - View workflow list

**Expected Results**:
- Interface map completed
- All navigation challenges completed
- Familiar with each functional area
- Successfully created first workflow

**Verification Method**:
- Check if interface map includes all main areas
- Check if can find all functions within 30 seconds
- Check if workflow list has newly created workflow

**Extended Challenge**:
- Explore workflow templates
- View execution history
- Try configuring credentials

**Troubleshooting**:
- **Problem**: Can't find a function
  - **Solution**: Check left sidebar, all main functions are there
- **Problem**: Interface display abnormal
  - **Solution**: Refresh page, check browser compatibility

### Exercise 4: Troubleshooting

**Task Objective**: Simulate common installation errors, practice solution steps, create troubleshooting checklist

**Prerequisites**:
- Completed Exercise 1, have basic understanding of N8N installation

**Detailed Steps**:

1. **Simulate Error 1: Port Occupied**
   - **Simulate**: Start another service occupying port 5678
   - **Error Symptom**: N8N cannot start, prompts port occupied
   - **Solution Steps**:
     - Check port occupancy: `netstat -ano | findstr 5678` (Windows) or `lsof -i :5678` (macOS/Linux)
     - Close program occupying port, or use another port
     - Set `N8N_PORT` environment variable to use new port
     - Restart N8N

2. **Simulate Error 2: Node.js Version Incompatible**
   - **Simulate**: Use old Node.js version (e.g., v12)
   - **Error Symptom**: Installation or startup fails, prompts version incompatible
   - **Solution Steps**:
     - Check Node.js version: `node --version`
     - Confirm need Node.js 16.0 or higher
     - Upgrade Node.js to LTS version
     - Reinstall N8N

3. **Simulate Error 3: Insufficient Permissions**
   - **Simulate**: Install in directory without permissions
   - **Error Symptom**: Installation fails, prompts insufficient permissions
   - **Solution Steps**:
     - Check current user permissions
     - Run with administrator privileges (Windows) or sudo (Linux/macOS)
     - Or choose directory with permissions for installation

4. **Create Troubleshooting Checklist**
   - List common errors
   - Provide solution steps for each error
   - Create quick reference table

**Expected Results**:
- Successfully simulated and solved 3 common errors
- Created complete troubleshooting checklist
- Understand solutions for common errors

**Verification Method**:
- Check if successfully solved simulated errors
- Check if troubleshooting checklist is complete
- Check if solution steps are clear

**Extended Challenge**:
- Research more common errors
- Create detailed troubleshooting documentation
- Share with other learners

**Troubleshooting Checklist Template**:

| Error Type | Error Symptom | Possible Cause | Solution Steps | Prevention |
|-----------|--------------|----------------|----------------|------------|
| Port Occupied | N8N cannot start | Another program occupying port | 1. Check port occupancy<br>2. Close occupying program or change port | Use fixed port, avoid conflicts |
| Node.js Version Incompatible | Installation fails | Node.js version too low | 1. Check version<br>2. Upgrade to 16.0+ | Use LTS version |
| Insufficient Permissions | Installation fails | Not enough permissions | 1. Check permissions<br>2. Use administrator privileges | Use directory with permissions |

## Common Questions

**Q1: Which installation method should I choose?**

A: It depends on your needs:
- **Quick experience**: Choose npx quick start
- **Personal long-term use**: Choose npm global installation or Docker
- **Team use**: Choose Docker Compose or cloud platform deployment
- **Production environment**: Choose cloud platform deployment

**Q2: Will npx method data be lost?**

A: Yes, npx method doesn't persistently save data by default. If you want to save data, you can set `N8N_USER_FOLDER` environment variable to specify data directory.

**Q3: How to change N8N's port?**

A: Use environment variable `N8N_PORT`:
```bash
# Windows PowerShell
$env:N8N_PORT=8080
npx n8n

# macOS/Linux
export N8N_PORT=8080
npx n8n
```

**Q4: How to make N8N run in background?**

A: Several ways:
- **Windows**: Use Task Scheduler or NSSM
- **macOS/Linux**: Use systemd or supervisor
- **Docker**: Use `docker-compose up -d` (run in background)

**Q5: How to update N8N?**

A: Depends on installation method:
- **npx**: Automatically uses latest version each run
- **npm**: Run `npm install -g n8n@latest`
- **Docker**: Run `docker-compose pull && docker-compose up -d`

**Q6: How to backup N8N data?**

A: Backup data directory (usually `~/.n8n` or `%USERPROFILE%\.n8n`):
- **Windows**: Copy `.n8n` folder
- **macOS/Linux**: Use `cp -r ~/.n8n ~/n8n-backup`
- **Docker**: Backup data volume

**Q7: How to configure N8N to use HTTPS?**

A: Need to:
1. Configure reverse proxy (such as Nginx)
2. Configure SSL certificate (can use Let's Encrypt)
3. Set `N8N_PROTOCOL=https`
4. Set `N8N_WEBHOOK_URL=https://your-domain.com`

**Q8: How much system resources does N8N need?**

A: Minimum requirements:
- CPU: 1 core
- Memory: 1GB RAM
- Storage: 1GB available space

Recommended configuration:
- CPU: 2 cores or more
- Memory: 2GB RAM or more
- Storage: 10GB or more

**Q9: Can I run multiple N8N instances on the same machine?**

A: Yes, but need to:
- Use different ports
- Use different data directories
- Ensure ports don't conflict

**Q10: How to uninstall N8N?**

A: Depends on installation method:
- **npx**: No need to uninstall, just delete data directory
- **npm**: Run `npm uninstall -g n8n`
- **Docker**: Run `docker-compose down -v` (delete data volume)

## Knowledge Check

### Multiple Choice Questions

1. **Which installation method is most suitable for technical beginners?**
   - A. Docker installation
   - B. npm global installation
   - C. npx quick start
   - D. Cloud platform deployment
   - **Answer**: C
   - **Explanation**: npx quick start is simplest, no installation needed, suitable for quick experience.

2. **Where is npx method data saved by default?**
   - A. Current directory
   - B. User directory
   - C. Not saved (lost after restart)
   - D. System directory
   - **Answer**: C
   - **Explanation**: npx method doesn't persistently save data by default, unless `N8N_USER_FOLDER` environment variable is set.

3. **How to change N8N's running port?**
   - A. Modify configuration file
   - B. Use environment variable `N8N_PORT`
   - C. Modify code
   - D. Cannot change
   - **Answer**: B
   - **Explanation**: Use environment variable `N8N_PORT` to change port.

4. **What are N8N's minimum system requirements?**
   - A. 2 core CPU, 4GB RAM
   - B. 1 core CPU, 1GB RAM
   - C. 4 core CPU, 8GB RAM
   - D. 8 core CPU, 16GB RAM
   - **Answer**: B
   - **Explanation**: N8N's minimum requirements are 1 core CPU and 1GB RAM.

5. **What is the advantage of Docker installation method?**
   - A. Simplest
   - B. Good isolation, easy to manage
   - C. No configuration needed
   - D. Data not persistent
   - **Answer**: B
   - **Explanation**: Docker provides good isolation and portability.

### Short Answer Questions

1. **List 4 main installation methods of N8N and explain their applicable scenarios.**

   **Sample Answer**:
   - **npx Quick Start**: Suitable for quick experience, testing, and learning
   - **npm Global Installation**: Suitable for personal long-term use, local development
   - **Docker Installation**: Suitable for users with Docker environment, need isolation
   - **Cloud Platform Deployment**: Suitable for production environment, team use

2. **How to configure N8N's basic authentication? Provide environment variable configuration examples.**

   **Sample Answer**:
   ```bash
   # Windows PowerShell
   $env:N8N_BASIC_AUTH_ACTIVE=true
   $env:N8N_BASIC_AUTH_USER=admin
   $env:N8N_BASIC_AUTH_PASSWORD=your-password
   
   # macOS/Linux
   export N8N_BASIC_AUTH_ACTIVE=true
   export N8N_BASIC_AUTH_USER=admin
   export N8N_BASIC_AUTH_PASSWORD=your-password
   ```

3. **What are the main areas of N8N's user interface? Briefly explain each area's function.**

   **Sample Answer**:
   - **Left Sidebar**: Contains workflow list, execution history, templates, credential management, settings
   - **Central Canvas**: Workflow design area for dragging nodes to create connections
   - **Right Panel**: Node configuration panel for setting node parameters
   - **Top Toolbar**: Contains save, execute, test, settings and other function buttons

4. **If you encounter a port occupied error, how should you solve it?**

   **Sample Answer**:
   1. Check port occupancy
   2. Close program occupying port or use another port
   3. Use `N8N_PORT` environment variable to set new port
   4. Restart N8N

5. **How to backup N8N data?**

   **Sample Answer**:
   - Backup data directory (usually `~/.n8n` or `%USERPROFILE%\.n8n`)
   - Windows: Copy `.n8n` folder
   - macOS/Linux: Use `cp -r ~/.n8n ~/n8n-backup`
   - Docker: Backup data volume

### Practice Questions

1. **Complete N8N Installation and Configuration**
   - Choose an installation method
   - Successfully install and start N8N
   - Complete basic configuration (account, environment variables, etc.)
   - Verify configuration is effective

2. **Create Interface Functional Area Map**
   - Open N8N interface
   - Draw interface map
   - Label each area's function
   - Complete interface navigation challenges

3. **Create Troubleshooting Checklist**
   - List at least 5 common errors
   - Provide solution steps for each error
   - Create quick reference table

## Further Reading

### Official Resources

1. **N8N Installation Documentation**
   - URL: https://docs.n8n.io/hosting/installation/
   - Content: Detailed installation guide, including various installation methods

2. **N8N Docker Documentation**
   - URL: https://docs.n8n.io/hosting/installation/docker/
   - Content: Detailed instructions for Docker installation and configuration

3. **N8N Environment Variables Reference**
   - URL: https://docs.n8n.io/reference/environment-variables/
   - Content: Detailed description of all environment variables

### Learning Resources

1. **Docker Official Documentation**
   - URL: https://docs.docker.com
   - Content: Docker basics and usage guide

2. **Node.js Official Documentation**
   - URL: https://nodejs.org/docs
   - Content: Node.js installation and usage guide

3. **Cloud Platform Deployment Guides**
   - DigitalOcean: https://www.digitalocean.com/community/tags/n8n
   - AWS: https://aws.amazon.com
   - Other cloud platform related documentation

### Related Tools and Concepts

1. **Docker Basics**
   - Understand Docker basic concepts
   - Learn Docker Compose usage
   - This will help you better use Docker method to install N8N

2. **Environment Variable Management**
   - Learn how to set environment variables in different operating systems
   - Learn environment variable best practices

3. **System Service Management**
   - Learn how to set applications as system services
   - Learn systemd (Linux) or Task Scheduler (Windows) usage

### Next Steps

After completing this chapter, it's recommended that you:

1. **Complete All Practice Exercises**
   - Ensure you've successfully installed N8N
   - Complete basic configuration
   - Familiarize yourself with N8N interface

2. **Prepare to Create First Workflow**
   - Next chapter will teach you how to create your first workflow
   - Ensure N8N is running normally

3. **Explore N8N Features**
   - Browse workflow templates
   - View execution history
   - Try creating simple workflows

4. **Start Chapter 3 Learning**
   - Next chapter will detail how to create your first workflow
   - Get ready to start your practical journey

---

## Quick Reference

### Installation Method Comparison

| Installation Method | Command | Data Persistent | Use Cases |
|---------------------|---------|-----------------|-----------|
| npx Quick Start | `npx n8n` | No (need config) | Quick experience |
| npm Global Installation | `npm install -g n8n` | Yes | Personal use |
| Docker Installation | `docker run n8nio/n8n` | Yes (need volume mount) | Have Docker environment |
| Cloud Platform Deployment | Per platform docs | Yes | Production environment |

### Common Environment Variables

| Environment Variable | Description | Example |
|---------------------|-------------|---------|
| `N8N_PORT` | Running port | `N8N_PORT=8080` |
| `N8N_HOST` | Bind host | `N8N_HOST=0.0.0.0` |
| `N8N_USER_FOLDER` | Data directory | `N8N_USER_FOLDER=~/n8n-data` |
| `N8N_BASIC_AUTH_ACTIVE` | Enable basic auth | `N8N_BASIC_AUTH_ACTIVE=true` |
| `N8N_BASIC_AUTH_USER` | Auth username | `N8N_BASIC_AUTH_USER=admin` |
| `N8N_BASIC_AUTH_PASSWORD` | Auth password | `N8N_BASIC_AUTH_PASSWORD=password` |

### System Requirements

- **Minimum Requirements**: 1 core CPU, 1GB RAM, 1GB storage
- **Recommended Configuration**: 2 core CPU, 2GB RAM, 10GB storage
- **Node.js Version**: 16.0 or higher (npm/npx method)

### Common Errors and Solutions

| Error | Cause | Solution |
|-------|-------|----------|
| Port Occupied | Another program occupying port | Change port or close occupying program |
| Node.js Version Incompatible | Version too low | Upgrade to 16.0+ |
| Insufficient Permissions | Not enough permissions | Use administrator privileges or change directory |
| Data Not Persistent | npx method not configured | Set `N8N_USER_FOLDER` |

---

**Congratulations on completing Chapter 2! Now you've successfully installed and configured N8N and familiarized yourself with the user interface. Are you ready to create your first workflow?** 🚀

