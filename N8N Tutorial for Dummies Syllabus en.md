# N8N Tutorial for Dummies Syllabus

> **Teaching Philosophy**: This tutorial adopts a goal-oriented teaching approach. Each chapter revolves around a core question, helping learners master N8N workflow automation skills through extensive hands-on practice.

---

## Chapter 1: What is N8N? Why Do I Need It?

**Core Question**: As a complete beginner, how can I understand what N8N is and how it solves my real-world problems?

**Learning Objectives**:
- Understand N8N's core concepts: workflow automation, nodes, connections
- Identify typical business scenarios that N8N can solve
- Compare N8N with other automation tools (such as Zapier, Make)
- Build initial awareness of N8N application scenarios

**Practice Tasks**:
1. **Scenario Analysis Exercise**: List 3-5 repetitive tasks in your daily work
2. **Tool Comparison Research**: Create a comparison table analyzing the pros and cons of N8N, Zapier, and Make
3. **Case Study**: Read 3 real-world N8N application cases and summarize the problems they solve
4. **Needs Assessment**: Complete a "My Automation Needs Checklist" with priority labels

**Assessment Criteria**:
- Able to clearly explain what N8N is
- Able to identify at least 5 scenarios suitable for using N8N
- Able to explain why to choose N8N over other tools

---

## Chapter 2: How to Install and Configure N8N from Scratch?

**Core Question**: As a technical novice, how can I successfully install N8N locally or in the cloud and perform basic configuration?

**Learning Objectives**:
- Master multiple installation methods for N8N (Docker, npm, npx, cloud services)
- Understand the applicable scenarios for different installation methods
- Complete N8N's initial configuration and account setup
- Familiarize with the basic layout and functional areas of the N8N user interface

**Practice Tasks**:
1. **Installation Practice** (choose one method):
   - Method A: Quick start using npx (recommended for beginners)
   - Method B: Install using Docker (recommended for users with Docker experience)
   - Method C: Global installation using npm
   - Method D: Deploy on cloud platforms (such as DigitalOcean, AWS)
2. **Configuration Exercise**:
   - Create administrator account
   - Configure environment variables
   - Set workflow storage location
   - Configure Webhook URL (if needed)
3. **Interface Exploration**:
   - Draw a functional area map of the N8N interface
   - Complete "Interface Navigation Challenge": Find 5 key functions within 30 seconds
4. **Troubleshooting**:
   - Simulate 3 common installation errors and practice resolution steps
   - Create a personal "Troubleshooting Checklist"

**Assessment Criteria**:
- Successfully install and start N8N
- Able to independently complete basic configuration
- Able to explain the purpose of each configuration option
- Able to solve at least 2 common installation problems

---

## Chapter 3: How to Create My First Workflow?

**Core Question**: How can I create a simple but complete workflow from scratch and understand the purpose of each step?

**Learning Objectives**:
- Understand the basic structure of workflows: Trigger → Process → Output
- Master methods for adding, connecting, and configuring nodes
- Learn to use workflow testing and execution functions
- Understand the meaning of workflow execution logs

**Practice Tasks**:
1. **Hello World Workflow**:
   - Create a schedule trigger (Schedule Trigger)
   - Add an HTTP Request node to call a public API (such as weather API)
   - Add a Set node to extract and format data
   - Add an Email node to send results (or use Webhook as output)
   - Execute and verify the workflow
2. **Data Flow Tracking Exercise**:
   - Create a workflow containing 5 nodes
   - Use "Execution History" to track data changes at each node
   - Draw a data flow diagram, labeling inputs and outputs of each node
3. **Error Handling Practice**:
   - Intentionally create a workflow that will fail
   - Learn to read error messages
   - Fix errors and re-execute
4. **Workflow Optimization**:
   - Create 3 different workflow implementations for the same task
   - Compare execution time and resource consumption
   - Choose the optimal solution and explain the reasoning

**Assessment Criteria**:
- Able to independently create a workflow containing at least 4 nodes
- Able to explain the purpose of each node in the workflow
- Able to read and understand execution logs
- Able to identify and fix common workflow errors

---

## Chapter 4: How to Connect and Use Third-Party Services?

**Core Question**: How can I connect N8N with my daily tools (such as Gmail, Slack, Google Sheets) to achieve true automation?

**Learning Objectives**:
- Understand N8N's authentication mechanisms (OAuth, API Key, etc.)
- Master connection configuration methods for commonly used services
- Learn to use Credential management functions
- Understand the purposes and limitations of different node types

**Practice Tasks**:
1. **Authentication Configuration Exercise**:
   - Configure Gmail OAuth authentication
   - Configure Slack Bot Token
   - Configure Google Sheets API Key
   - Configure a service requiring custom authentication
   - Create a personal "Authentication Configuration Quick Reference"
2. **Integration Project 1 - Email Automation**:
   - Create a workflow: When receiving emails with specific subjects, automatically extract attachments and save to Google Drive
   - Add conditional judgment: Execute different operations based on different senders
   - Add notification: Send Slack message upon completion
3. **Integration Project 2 - Data Synchronization**:
   - Create a workflow: Fetch data from API on a daily schedule
   - Write data to Google Sheets
   - If data changes exceed threshold, send alert email
4. **Integration Project 3 - Cross-Platform Notifications**:
   - Create a workflow: Monitor website status
   - If website is down, simultaneously send email, Slack message, and SMS (using Twilio)
5. **Credential Management**:
   - Create, edit, delete Credentials
   - Understand Credential scope and security
   - Practice sharing Credentials across different workflows

**Assessment Criteria**:
- Able to successfully configure authentication for at least 5 different services
- Able to create workflows integrating at least 3 third-party services
- Able to explain the difference between OAuth and API Key
- Able to independently solve common authentication-related problems

---

## Chapter 5: How to Process and Transform Data?

**Core Question**: When data flows in from different sources, how can I clean, transform, merge, and format this data to meet my needs?

**Learning Objectives**:
- Understand N8N's data structure (JSON format)
- Master commonly used data operation nodes (Set, Code, Function, Item Lists, etc.)
- Learn to use N8N expression language
- Master advanced operations such as data aggregation, filtering, sorting

**Practice Tasks**:
1. **Data Extraction Exercise**:
   - Extract nested data from a complex JSON response
   - Use expressions to extract specific elements from arrays
   - Create reusable data extraction templates
2. **Data Transformation Practice**:
   - Create a workflow: Fetch raw data from API
   - Use Set node to rename fields
   - Use Code node for data calculation and formatting
   - Use Function node to implement complex data transformation logic
3. **Data Merging Project**:
   - Fetch data from 3 different APIs
   - Use Merge node to combine data
   - Handle data conflicts and missing fields
   - Output unified JSON format
4. **Data Filtering and Conditional Processing**:
   - Create a workflow: Process 100 data records
   - Use IF node to route data based on conditions
   - Execute operation A for data meeting conditions, operation B for those not meeting conditions
   - Count the number of each case
5. **Expression Language Deep Practice**:
   - Complete 20 expression exercises (date formatting, string operations, mathematical calculations, etc.)
   - Create a personal "Expression Quick Reference Manual"
   - Implement a complex expression: combine multiple data sources, perform conditional judgment and calculation
6. **Array and Batch Processing**:
   - Understand the role of Split In Batches node
   - Create a workflow: Process large amounts of data in batches to avoid timeouts
   - Implement error retry mechanism

**Assessment Criteria**:
- Able to use expressions to extract and manipulate JSON data
- Able to independently write at least 10 commonly used data transformation expressions
- Able to create complex workflows including data merging, filtering, and transformation
- Able to explain the data flow process between nodes

---

## Chapter 6: How to Implement Conditional Logic and Loop Control?

**Core Question**: When my workflow needs to execute different operations based on different conditions, or needs to repeatedly process multiple items, how can I implement these logics?

**Learning Objectives**:
- Understand usage scenarios of conditional nodes
- Master the differences and usage of IF node and Switch node
- Learn to use Loop nodes to process array data
- Understand workflow execution flow control

**Practice Tasks**:
1. **Conditional Judgment Basics**:
   - Create a workflow: Execute 3 different paths based on different input data values
   - Use IF node to implement simple conditions
   - Use Switch node to implement multi-branch conditions
   - Compare applicable scenarios of both methods
2. **Nested Condition Exercise**:
   - Create a complex conditional judgment workflow
   - Implement 3-level nested conditional logic
   - Draw conditional decision tree
   - Test all possible condition combinations
3. **Loop Processing Practice**:
   - Create a workflow: Process an array containing 100 items
   - Use Loop Over Items node to iterate through each item
   - Execute the same operation for each item (such as sending email)
   - Add progress tracking and error handling
4. **Condition + Loop Combination Project**:
   - Create a workflow: Fetch order list from API
   - Iterate through each order
   - Execute different operations based on order status (pending, shipped, completed)
   - Count orders in each status
5. **Error Handling and Retry Logic**:
   - Create a workflow that may fail
   - Implement error capture and retry mechanism
   - Use Continue On Fail option
   - Create error notification mechanism
6. **Workflow Pause and Resume**:
   - Create a workflow requiring manual approval
   - Use Wait node to pause execution
   - Implement approval pass/reject branch logic

**Assessment Criteria**:
- Able to create workflows containing at least 3 levels of conditional judgment
- Able to use loop nodes to process array data
- Able to implement error handling and retry logic
- Able to draw and explain execution flow diagrams of complex workflows

---

## Chapter 7: How to Debug and Optimize Workflows?

**Core Question**: When my workflow encounters errors or runs slowly, how can I quickly locate problems and optimize performance?

**Learning Objectives**:
- Master N8N's debugging tools and methods
- Learn to read and analyze execution logs
- Understand principles of workflow performance optimization
- Master diagnosis and resolution methods for common errors

**Practice Tasks**:
1. **Debugging Tool Exploration**:
   - Use "Execution History" to view workflow execution records
   - Use "Test Workflow" function for step-by-step debugging
   - Use "Pause Execution" function to pause at specific nodes
   - Create a personal "Debugging Checklist"
2. **Log Analysis Exercise**:
   - Intentionally create 5 different types of errors
   - Analyze log information for each error type
   - Create "Error Log Interpretation Guide"
   - Practice quickly locating problem nodes from logs
3. **Performance Optimization Practice**:
   - Create a slow workflow containing 10 nodes
   - Use execution time analysis to find bottleneck nodes
   - Optimize workflow: merge nodes, reduce API calls, use caching
   - Compare execution time before and after optimization
4. **Error Handling Best Practices**:
   - Create a workflow containing multiple potential failure points
   - Add error handling for each critical node
   - Implement error notification and logging
   - Create error recovery mechanism
5. **Workflow Testing Strategy**:
   - Create test datasets
   - Implement unit testing: test functionality of individual nodes
   - Implement integration testing: test entire workflow
   - Create test report template
6. **Monitoring and Alerting**:
   - Set up workflow execution monitoring
   - Create failure alert mechanism
   - Implement execution statistics and reporting

**Assessment Criteria**:
- Able to independently debug and fix workflow errors
- Able to analyze execution logs and locate problems
- Able to optimize workflow performance, reducing execution time by at least 30%
- Able to create complete error handling and monitoring mechanisms

---

## Chapter 8: How to Deploy and Maintain N8N in Production?

**Core Question**: When my workflow development is complete, how can I deploy it to production and ensure stable operation and continuous maintenance?

**Learning Objectives**:
- Understand the difference between production and development environments
- Master N8N deployment options and best practices
- Learn to configure backup and recovery mechanisms
- Understand version control and update strategies

**Practice Tasks**:
1. **Deployment Solution Comparison**:
   - Research 5 N8N deployment solutions (local, Docker, cloud services, Kubernetes, etc.)
   - Create comparison table: cost, complexity, scalability, security
   - Choose the most suitable deployment solution for different scenarios
2. **Production Environment Configuration**:
   - Configure environment variable management
   - Set up database (PostgreSQL/MySQL)
   - Configure reverse proxy (Nginx)
   - Set up SSL certificate
   - Configure firewall and security rules
3. **Backup and Recovery Practice**:
   - Create automated backup script
   - Test backup recovery process
   - Create "Disaster Recovery Plan"
   - Implement regular backup verification
4. **Version Control**:
   - Use Git to manage workflow code
   - Create workflow version management process
   - Implement workflow rollback mechanism
5. **Monitoring and Maintenance**:
   - Set up system monitoring (CPU, memory, disk)
   - Configure log aggregation and analysis
   - Create maintenance checklist
   - Implement automated health checks
6. **Security Hardening**:
   - Configure user permission management
   - Implement API access control
   - Set up audit logs
   - Perform security vulnerability scanning

**Assessment Criteria**:
- Able to independently deploy N8N to production environment
- Able to configure complete backup and recovery mechanisms
- Able to establish workflow version management process
- Able to implement basic security hardening measures

---

## Chapter 9: How to Build AI-Driven Workflows?

**Core Question**: How can I integrate AI capabilities (such as ChatGPT, image recognition, text analysis) into my workflows to achieve intelligent automation?

**Learning Objectives**:
- Understand N8N's AI nodes and integration capabilities
- Master integration methods for AI services like OpenAI, Anthropic
- Learn to build AI-driven automation scenarios
- Understand design patterns and best practices for AI workflows

**Practice Tasks**:
1. **AI Service Integration Basics**:
   - Configure OpenAI API authentication
   - Configure Anthropic Claude API
   - Test basic AI node functionality
   - Create "AI Service Comparison Table"
2. **Text Generation Workflow**:
   - Create a workflow: Fetch news from RSS feed daily
   - Use AI node to generate news summaries
   - Generate social media posts based on summaries
   - Automatically publish to Twitter/LinkedIn
3. **Content Analysis and Classification**:
   - Create a workflow: Receive user feedback emails
   - Use AI to analyze sentiment
   - Route to different processing flows based on sentiment classification
   - Generate analysis reports
4. **Intelligent Data Processing**:
   - Create a workflow: Fetch unstructured data from database
   - Use AI to extract key information
   - Structure and store extracted information
   - Implement data quality checks
5. **AI Agent Workflow**:
   - Create an AI assistant workflow
   - Implement multi-turn conversation capability
   - Integrate knowledge base retrieval
   - Implement context memory functionality
6. **Image and Multimedia Processing**:
   - Integrate image recognition API
   - Create automatic image labeling workflow
   - Implement video content analysis process

**Assessment Criteria**:
- Able to successfully integrate at least 2 AI services
- Able to create complete workflows with AI functionality
- Able to explain how AI nodes work
- Able to optimize cost and performance of AI workflows

---

## Chapter 10: How to Build Complex Business Automation Solutions?

**Core Question**: When I need to automate a complete business process, how can I design, implement, and manage a complex automation solution containing multiple workflows and involving multiple systems?

**Learning Objectives**:
- Understand architecture design of complex automation systems
- Master communication and coordination methods between workflows
- Learn to design scalable and maintainable automation systems
- Understand best practices for business process automation

**Practice Tasks**:
1. **System Architecture Design**:
   - Choose a complex business process (such as customer onboarding, order processing, content publishing, etc.)
   - Draw system architecture diagram
   - Identify workflows that need automation
   - Design data flow and trigger relationships between workflows
2. **Multi-Workflow Coordination Project**:
   - Create 3 interconnected workflows
   - Implement Workflow A triggering Workflow B
   - Implement parallel execution of Workflow B and Workflow C
   - Implement data sharing between workflows
3. **Error Handling and Recovery**:
   - Design global error handling mechanism
   - Implement automatic retry when workflows fail
   - Create error notification and escalation process
   - Implement data consistency guarantees
4. **Performance Optimization and Scaling**:
   - Identify system bottlenecks
   - Implement load balancing for workflows
   - Optimize database queries and API calls
   - Design horizontal scaling solution
5. **Monitoring and Reporting**:
   - Create unified monitoring dashboard
   - Implement business metrics tracking
   - Generate automation execution reports
   - Set up alerting and notification mechanisms
6. **Documentation and Maintenance**:
   - Write system architecture documentation
   - Create workflow operation manual
   - Establish change management process
   - Design knowledge transfer mechanism

**Assessment Criteria**:
- Able to design automation systems containing at least 5 interconnected workflows
- Able to implement coordination and communication between workflows
- Able to establish complete monitoring and maintenance mechanisms
- Able to write clear system documentation

---

## Chapter 11: How to Solve Real Business Problems?

**Core Question**: Facing real business needs, how can I use N8N skills to completely solve a real problem, from requirements analysis to solution implementation?

**Learning Objectives**:
- Master the complete process from requirements to implementation
- Learn requirements analysis and solution design
- Understand the complexity of business scenarios and trade-offs in solutions
- Develop ability to independently solve real-world problems

**Practice Tasks** (Complete 3-5 real scenarios):

1. **Scenario 1: Customer Support Automation**
   - Requirement: Automatically process customer support tickets, route by priority and type, generate replies, update CRM
   - Task: Fully implement this automation process, including error handling and monitoring

2. **Scenario 2: Content Marketing Automation**
   - Requirement: Automatically collect industry news, AI generate content, multi-platform publishing, track effectiveness
   - Task: Design and implement complete content marketing automation pipeline

3. **Scenario 3: Data Report Automation**
   - Requirement: Collect data from multiple sources, clean and integrate, generate visual reports, scheduled sending
   - Task: Create end-to-end data report automation system

4. **Scenario 4: Inventory Management Automation**
   - Requirement: Monitor inventory levels, automatic replenishment, update multiple systems, send notifications
   - Task: Implement intelligent inventory management system

5. **Scenario 5: Employee Onboarding Automation**
   - Requirement: When new employees onboard, automatically create accounts, assign permissions, send welcome emails, schedule training
   - Task: Build complete employee onboarding automation process

**Completion Requirements for Each Scenario**:
- Requirements analysis and documentation
- System design and technology selection
- Workflow development and testing
- Deployment and monitoring configuration
- User training and documentation
- Project summary and experience sharing

**Assessment Criteria**:
- Able to independently complete automation for at least 3 real business scenarios
- Able to write clear requirements documents and design solutions
- Able to handle complex problems during implementation
- Able to evaluate solution effectiveness and improvement directions

---

## Chapter 12: How to Build an Enterprise-Grade Intelligent Contract Processing Automation System?

**Core Question**: Facing the complex multi-step process of enterprise contract processing involving "attachment extraction → text parsing → compliance validation → risk annotation → report generation → approval workflow", how can I use N8N combined with LangGraph, Langdock, Microsoft CoPilot and other advanced technologies to build an intelligent automation system with visual orchestration, tool integration, dynamic adjustment, and high fault tolerance?

**Learning Objectives**:
- Understand architecture design principles for enterprise-grade automation systems
- Master integration methods for N8N with LangGraph, Langdock, and Microsoft CoPilot
- Learn to design complex workflows with multi-tool collaboration
- Master dynamic flow control and context management techniques
- Understand design and implementation of high-fault-tolerance exception handling mechanisms
- Learn to build intelligent interaction and observability systems

**Practice Tasks**:

1. **System Architecture Design and Technology Selection**:
   - Analyze business requirements and technical challenges of contract processing workflows
   - Design system architecture based on N8N + LangGraph + Langdock + CoPilot
   - Draw system component diagrams and data flow diagrams
   - Create technology stack comparison table, explaining responsibilities and advantages of each technology
   - Design tool interface specifications and data transfer formats

2. **Visual Workflow Definition (Based on N8N)**:
   - Create main contract processing workflow in N8N, including the following core steps:
     - Attachment capture node (extract contract files from specified folder, support docx, pdf, image formats)
     - Contract text parsing node (dynamically select parsing tool based on file format)
     - Compliance regulation retrieval node (retrieve relevant regulations based on parsed contract clauses)
     - Risk assessment node (analyze conflicts between clauses and regulations, annotate risk levels)
     - Report generation node (integrate parsing results, compliance conclusions, risk points, generate approval reports)
     - Approval workflow node (route to different approval processes based on risk level)
   - Configure step dependencies (e.g., "compliance retrieval" depends on "text parsing" output)
   - Implement serial and parallel execution modes (e.g., "parse contract text" simultaneously with "extract contract key information")

3. **Tool Registration and Flexible Integration (Based on Langdock)**:
   - Register at least 4 core tool types through Langdock, implementing standard interface (run(input, context)):
     - Document parsing tool (support docx/pdf text extraction)
     - OCR parsing tool (support image contract recognition)
     - Regulation retrieval tool (integrate Mock regulation database)
     - Risk assessment tool (analyze conflicts between contract text and regulation provisions)
   - Implement enterprise information query API (Mock)
   - Test standard interface calls and data return formats
   - Create tool registration and configuration documentation

4. **Dynamic Flow Control and Context Management (Based on LangGraph)**:
   - Use LangGraph to define workflow nodes and state transitions
   - Implement conditional branch logic:
     - Format branch: Dynamically select "document parsing tool" or "OCR tool" based on contract file format (text/image)
     - Risk branch: High risk enters "legal manual approval" node; medium/low risk enters "automatic electronic approval" node
     - Retrieval branch: Automatically supplement keywords and retry when regulation retrieval results are insufficient, trigger CoPilot prompt after 2 retries still fail
   - Implement context management: Save intermediate results throughout the process, support cross-step data transfer
   - Implement context expiration cleanup mechanism (automatically delete after 24 hours after process completion)

5. **Custom Compliance Rule Implementation**:
   - Implement 3 types of compliance rule checks:
     - Penalty ratio check (exceeding 30% of total contract amount is violation)
     - Statute of limitations check (agreed limitation <3 years or <1 year is violation)
     - Dispute resolution method conflict check (simultaneously agreeing to arbitration and litigation is violation)
   - Implement compliance judgment logic: No conflicts or conflicts with legal exception explanations are compliant, otherwise violation
   - Implement violation handling: Annotate high risk, cite specific regulation provisions, provide modification suggestions, jump to legal manual modification process

6. **High-Fault-Tolerance Exception Handling Mechanism**:
   - Implement automatic retry on step failure: Configure retry count (default 2 times) and interval (default 30 seconds)
   - Implement backup tool switching: Automatically switch to backup tool when primary tool fails
   - Implement exception alerting and manual intervention: Push alerts to administrators through CoPilot after critical steps fail continuously
   - Create error handling flow diagram and troubleshooting manual

7. **Intelligent Interaction and Observability (Based on Microsoft CoPilot)**:
   - Implement CoPilot natural language interaction:
     - Support triggering tasks through natural language (e.g., "process sales contracts from December 2025 in folder")
     - Support querying process status (e.g., "which step is the current contract approval at")
     - Support obtaining exception handling suggestions (e.g., "what to do if parsing fails")
   - Implement execution log recording: Display input, output, duration, tool call details, error information for each step
   - Implement process visualization: Generate task flow diagrams (including execution paths, branch directions, node status), support export as images

8. **End-to-End Testing and Optimization**:
   - Prepare test datasets: Include contract files in different formats (docx, pdf, images)
   - Test complete process: Full workflow testing from attachment capture to approval workflow
   - Test exception scenarios: Tool failures, network timeouts, data format errors, etc.
   - Performance optimization: Identify bottleneck nodes, optimize execution time
   - Create test reports and performance analysis documentation

9. **System Deployment and Documentation**:
   - Configure production environment: Environment variables, database, reverse proxy, SSL certificate
   - Implement monitoring and alerting mechanisms
   - Write system architecture documentation
   - Write user operation manual
   - Write API interface documentation
   - Create deployment and maintenance guide

**Assessment Criteria**:
- Able to design and implement complex workflows containing at least 6 core steps
- Able to successfully integrate four technologies: N8N, LangGraph, Langdock, Microsoft CoPilot
- Able to implement at least 3 types of conditional branch logic and dynamic flow control
- Able to implement complete fault tolerance mechanisms, including retry, backup tool switching, exception alerting
- Able to implement custom compliance rule checks, accurately identify violation clauses
- Able to implement natural language interaction and process visualization through CoPilot
- Able to write complete technical documentation and user manuals
- System can run stably, processing at least 10 contract files of different types

---

## Appendix A: Common Nodes Quick Reference

**Core Question**: When I need to quickly find usage information for a node, how can I quickly find reference information?

**Content**:
- Trigger node list and usage scenarios
- Operation node list and configuration points
- Data transformation nodes and expression examples
- Common expression function reference
- Error codes and solution quick reference

---

## Appendix B: Best Practices and Design Patterns

**Core Question**: How to avoid common errors and adopt industry best practices to design workflows?

**Content**:
- Workflow naming and organization standards
- Data security best practices
- Performance optimization techniques
- Error handling patterns
- Maintainability design principles
- Security and compliance considerations

---

## Appendix C: Troubleshooting Guide

**Core Question**: When encountering problems, how can I quickly find solutions?

**Content**:
- Common errors and solutions
- Debugging techniques and tools
- Community resources and help channels
- Problem reporting template

---

## Learning Path Recommendations

### Beginner Path (4-6 weeks)
- Chapters 1-3: Basic Introduction (1 week)
- Chapter 4: Service Integration (1 week)
- Chapter 5: Data Processing (1 week)
- Chapter 6: Logic Control (1 week)
- Chapter 7: Debugging and Optimization (1 week)
- Practice Project: Complete 2-3 simple automation scenarios (1 week)

### Intermediate Path (6-8 weeks)
- Complete Beginner Path
- Chapter 8: Production Deployment (1 week)
- Chapter 9: AI Integration (1-2 weeks)
- Chapter 10: Complex Systems (2 weeks)
- Chapter 11: Practical Projects (2-3 weeks)
- Chapter 12: Enterprise-Grade Intelligent Contract Processing System (3-4 weeks)

### Expert Path (Continuous Learning)
- Complete Intermediate Path
- Deep research into N8N advanced features
- Contribute to open source projects
- Share experiences and best practices
- Continuously follow N8N updates and new features

---

## Assessment and Certification

### Self-Assessment Checklist
After completing each chapter, check the following items:
- [ ] I can independently complete all practice tasks in this chapter
- [ ] I can explain the core concepts of this chapter to others
- [ ] I can solve common problems related to this chapter
- [ ] I can apply the knowledge from this chapter to real scenarios

### Project Portfolio
It is recommended to create a workflow project for each important chapter to form a personal portfolio:
- Project 1: Multi-service integration workflow
- Project 2: Data processing and transformation workflow
- Project 3: Conditional logic and loop workflow
- Project 4: AI-driven workflow
- Project 5: Complex business automation system
- Project 6: Enterprise-Grade Intelligent Contract Processing Automation System (Comprehensive Project)

### Final Assessment
Complete the following tasks to demonstrate mastery:
1. Independently design and implement a complete business automation solution
2. Write detailed technical documentation and user manual
3. Conduct solution demonstration and Q&A
4. Submit project summary and improvement suggestions

---

## Usage Instructions

This tutorial syllabus adopts a goal-oriented teaching approach, with each chapter revolving around a core question. Learners are advised to:

1. **Learn in Order**: Chapters have progressive relationships, it is recommended to complete them in order
2. **Emphasize Practice**: Practice tasks in each chapter are mandatory, do not skip them
3. **Take Notes**: It is recommended to create personal learning notes, recording key concepts and practical experience
4. **Build Portfolio**: Create actual workflows for each important chapter to form a portfolio
5. **Participate in Community**: Actively seek help and share experiences when encountering problems

**Happy Learning! Start Your N8N Automation Journey!** 🚀

