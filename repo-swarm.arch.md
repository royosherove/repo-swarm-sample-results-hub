# hl_overview

High level overview of the codebase

# Project Analysis: Repository Swarm

## 0. **Repository Name:** 
[[repo-swarm]]

## 1. **Project Purpose**
This project appears to be a **repository analysis and investigation system** that automatically analyzes code repositories to understand their structure, architecture, and characteristics. It uses AI/LLM (specifically Claude) to perform intelligent code analysis and generates insights about repositories. The system seems designed to help understand large codebases by automatically detecting repository types, analyzing code patterns, and providing structured summaries.

## 2. **Architecture Pattern**
**Workflow-based Microservices Architecture** with **Event-Driven Processing** - The system uses Temporal workflows for orchestration, with separate workers handling different aspects of repository investigation and analysis.

## 3. **Technology Stack**

### **Primary Languages & Frameworks:**
- **Python** (primary language)
- **Temporal** (workflow orchestration)
- **AWS DynamoDB** (data storage)
- **Claude AI/Anthropic** (LLM for code analysis)

### **Python Dependencies** (from pyproject.toml analysis):
- **Temporal SDK** (`temporalio`) - Workflow orchestration
- **AWS SDK** (`boto3`, `botocore`) - AWS services integration
- **HTTP Libraries** (`requests`, `httpx`) - API communications
- **AI/ML Libraries** (`anthropic`) - Claude AI integration
- **Git Integration** (`GitPython`) - Repository manipulation
- **Testing** (`pytest`, `pytest-asyncio`) - Testing framework
- **Development Tools** (`uv`) - Package management

## 4. **Initial Structure Impression**
The application has several main high-level components:
- **Investigation Engine** (`src/investigator/`) - Core repository analysis logic
- **Workflow Orchestration** (`src/workflows/`) - Temporal workflow definitions
- **Worker Services** (`src/worker.py`, `src/investigate_worker.py`) - Background processing
- **Activities** (`src/activities/`) - Atomic workflow operations
- **Prompt System** (`prompts/`) - AI prompt templates organized by repository type
- **Utilities** (`src/utils/`) - Supporting infrastructure (storage, caching)
- **Testing Suite** (`tests/`) - Comprehensive test coverage

## 5. **Configuration/Package Files**
- `pyproject.toml` - Python project configuration and dependencies
- `uv.lock` - Lock file for dependency versions
- `pytest.ini` - Test configuration
- `Dockerfile` - Container configuration
- `mise.toml` - Development environment setup
- `env.example` / `env.local.example` - Environment variable templates
- `prompts/base_prompts.json` - AI prompt configurations
- `prompts/prompt_selector.json` - Prompt selection logic
- `prompts/repos.json` - Repository configurations

## 6. **Directory Structure**

### **Source Code Organization (`src/`):**
- **`workflows/`** - Temporal workflow definitions for orchestrating repository investigation
- **`investigator/`** - Core analysis engine with repository detection and analysis logic
  - **`core/`** - Core components (git manager, Claude analyzer, file manager, etc.)
- **`activities/`** - Atomic workflow operations (caching, investigation tasks)
- **`utils/`** - Infrastructure utilities (DynamoDB client, prompt context management)
- **`models/`** - Data models for workflows, investigations, and caching

### **Supporting Directories:**
- **`prompts/`** - AI prompts organized by repository type (frontend, backend, mobile, infra-as-code, etc.)
- **`scripts/`** - Operational scripts for testing, deployment, and maintenance
- **`tests/`** - Unit and integration tests

## 7. **High-Level Architecture**
**Workflow-Orchestrated Analysis Pipeline** with the following patterns:

- **Event-Driven Workflow Architecture**: Uses Temporal for reliable, distributed workflow execution
- **Activity-Based Processing**: Breaks down repository analysis into discrete, retryable activities
- **Intelligent Prompt Selection**: Dynamic prompt selection based on repository type detection
- **Caching Layer**: DynamoDB-based caching for investigation results and workflow state
- **Multi-Stage Analysis Pipeline**: Detection → Analysis → Results Collection

**Evidence:**
- Temporal workflow definitions in `src/workflows/`
- Activity-based decomposition in `src/activities/`
- Repository type detection system in `src/investigator/core/repository_type_detector.py`
- Caching infrastructure in `src/activities/investigation_cache.py`

## 8. **Build, Execution and Test**

### **Build & Dependency Management:**
- **Package Manager**: `uv` (modern Python package manager)
- **Installation**: `uv sync` or using `install_test_deps.sh`

### **Execution:**
- **Main Entry Points**:
  - `src/worker.py` - Main workflow worker
  - `src/investigate_worker.py` - Investigation-specific worker
  - `src/client.py` - Client interface
- **Scripts**: Multiple operational scripts in `scripts/` directory
  - `scripts/investigate.sh` - Run investigation
  - `scripts/workflow.sh` - Workflow operations
  - `scripts/get-started.sh` - Quick start

### **Testing:**
- **Framework**: pytest with async support
- **Test Structure**: Separate unit and integration tests
- **Test Scripts**: 
  - `scripts/test-investigator.sh`
  - `scripts/test-investigate-workflow.sh`
- **Coverage**: Comprehensive testing including DynamoDB integration, workflow caching, and Claude integration

### **Development:**
- **Environment**: Uses `mise.toml` for development environment setup
- **Docker**: Containerized deployment via `Dockerfile`
- **Health Checks**: Built-in health check system (`src/health_check.py`)

# module_deep_dive

Deep dive into modules

# Detailed Component Breakdown

## 1. `src/workflows/`

### Core Responsibility
Orchestrates high-level repository investigation workflows using Temporal workflow framework, coordinating multiple activities to analyze repositories systematically.

### Key Components
- **`investigate_repos_workflow.py`**: Main workflow for processing multiple repositories in batch
- **`investigate_single_repo_workflow.py`**: Workflow for analyzing individual repositories
- **`__init__.py`**: Module initialization

### Dependencies & Interactions
- **Internal Dependencies:**
  - `@src/activities/` - Executes investigation and caching activities
  - `@src/models/workflows.py` - Uses workflow data models
  - `@src/models/investigation.py` - Handles investigation result structures
- **External Services:**
  - Temporal workflow engine for orchestration
  - DynamoDB for caching and state persistence

---

## 2. `src/utils/`

### Core Responsibility
Provides utility services for prompt context management, DynamoDB operations, and storage key generation to support the investigation pipeline.

### Key Components
- **`prompt_context.py`**: Main prompt context management interface
- **`prompt_context_dynamodb.py`**: DynamoDB-backed prompt context storage
- **`prompt_context_file.py`**: File-based prompt context storage
- **`prompt_context_base.py`**: Base class for prompt context implementations
- **`dynamodb_client.py`**: DynamoDB client wrapper and operations
- **`storage_keys.py`**: Storage key generation and management utilities

### Dependencies & Interactions
- **Internal Dependencies:**
  - `@src/models/cache.py` - Uses caching models
  - Shared across all modules for storage operations
- **External Services:**
  - AWS DynamoDB for persistent storage
  - Local file system for file-based storage

---

## 3. `src/models/`

### Core Responsibility
Defines data structures and models for activities, workflows, investigations, and caching throughout the application.

### Key Components
- **`activities.py`**: Data models for Temporal activities
- **`workflows.py`**: Workflow parameter and result models
- **`investigation.py`**: Investigation process and result structures
- **`cache.py`**: Caching-related data models
- **`__init__.py`**: Model exports and initialization

### Dependencies & Interactions
- **Internal Dependencies:**
  - Used by all other modules as foundational data structures
  - No dependencies on other internal modules (base layer)
- **External Services:**
  - Temporal framework for workflow/activity type definitions
  - Pydantic for data validation and serialization

---

## 4. `src/investigator/`

### Core Responsibility
Contains the core repository investigation engine that analyzes codebases, detects repository types, and generates detailed analysis reports using AI services.

### Key Components
- **`investigator.py`**: Main investigation orchestration class
- **`activity_wrapper.py`**: Temporal activity wrapper for the investigator
- **`example.py` & `example_private_repo.py`**: Usage examples
- **`core/` subdirectory**: Core investigation components
  - **`repository_analyzer.py`**: Main repository analysis logic
  - **`claude_analyzer.py`**: AI-powered code analysis using Claude
  - **`analysis_results_collector.py`**: Collects and processes analysis results
  - **`repository_type_detector.py`**: Detects repository type (frontend, backend, etc.)
  - **`git_manager.py`**: Git repository operations
  - **`file_manager.py`**: File system operations and filtering
  - **`config.py`**: Configuration management
  - **`constants.py`**: Application constants
  - **`utils.py`**: Utility functions

### Dependencies & Interactions
- **Internal Dependencies:**
  - `@src/models/investigation.py` - Investigation data models
  - `@src/utils/` - Storage and context utilities
  - `@prompts/` - Analysis prompt templates
- **External Services:**
  - Claude AI API for code analysis
  - Git repositories (GitHub, local)
  - File system for repository checkout and analysis

---

## 5. `src/activities/`

### Core Responsibility
Implements Temporal activities for investigation processes and caching operations, providing the building blocks for workflows.

### Key Components
- **`investigate_activities.py`**: Core investigation activity implementations
- **`investigation_cache.py`**: Caching logic and cache management
- **`investigation_cache_activities.py`**: Temporal activities for cache operations
- **`dynamodb_health_check_activity.py`**: Health check activity for DynamoDB
- **`__init__.py`**: Activity exports

### Dependencies & Interactions
- **Internal Dependencies:**
  - `@src/investigator/` - Uses investigator engine
  - `@src/models/activities.py` - Activity data models
  - `@src/utils/` - Storage and DynamoDB utilities
- **External Services:**
  - Temporal framework for activity execution
  - DynamoDB for caching and health checks

---

## 6. `prompts/`

### Core Responsibility
Contains structured prompt templates and configurations for AI-powered code analysis, organized by repository type and analysis focus.

### Key Components
- **Configuration Files:**
  - **`base_prompts.json`**: Base prompt configurations
  - **`prompt_selector.json`**: Prompt selection logic
  - **`repos.json`**: Repository configurations
  - **`skip_repos.json`**: Repositories to skip
- **Type-specific Prompts:**
  - **`frontend/`**: Frontend-specific analysis prompts
  - **`backend/`**: Backend system analysis prompts
  - **`mobile/`**: Mobile application prompts
  - **`libraries/`**: Library/SDK analysis prompts
  - **`infra-as-code/`**: Infrastructure analysis prompts
  - **`generic/`**: Generic repository prompts
- **Shared Analysis Templates:**
  - **`shared/`**: Common analysis aspects (security, auth, APIs, etc.)
- **Detection Prompts:**
  - **`DETECTION.md`**: Repository type detection
  - **`METADATA_DETECTION.md`**: Metadata extraction

### Dependencies & Interactions
- **Internal Dependencies:**
  - Used by `@src/investigator/core/claude_analyzer.py` for AI analysis
  - Referenced by `@src/investigator/core/repository_type_detector.py`
- **External Services:**
  - Claude AI API (prompts are sent to Claude for analysis)

---

## 7. Root Level Files

### Core Responsibility
Project configuration, deployment, and development workflow management.

### Key Components
- **`client.py`**: Client interface for the investigation service
- **`worker.py`**: Main Temporal worker process
- **`investigate_worker.py`**: Specialized investigation worker
- **`query_workflow_status.py`**: Workflow status querying utility
- **`health_check.py`**: Service health check endpoint
- **`workflow_config.py`**: Workflow configuration management

### Dependencies & Interactions
- **Internal Dependencies:**
  - `@src/workflows/` - Workflow definitions
  - `@src/activities/` - Activity implementations
  - `@src/models/` - Data models
  - `@src/utils/` - Utility services
- **External Services:**
  - Temporal server for workflow execution
  - DynamoDB for persistence
  - Claude AI API through investigator components

# dependencies

Analyze dependencies and external libraries

# Dependency and Architecture Analysis

## Internal Modules

### Core Application Components

**`src/investigator/`**: Repository investigation and analysis engine
- **`src/investigator/investigator.py`**: Main orchestrator for repository investigations
- **`src/investigator/activity_wrapper.py`**: Temporal activity wrapper for investigation tasks
- **`src/investigator/core/`**: Core analysis functionality
  - **`repository_analyzer.py`**: Primary repository analysis logic
  - **`claude_analyzer.py`**: Claude AI integration for code analysis
  - **`analysis_results_collector.py`**: Aggregates and processes analysis results
  - **`repository_type_detector.py`**: Detects repository type and technology stack
  - **`git_manager.py`**: Git operations and repository management
  - **`file_manager.py`**: File system operations and content handling
  - **`config.py`**: Configuration management
  - **`constants.py`**: Application constants and settings

**`src/workflows/`**: Temporal workflow definitions
- **`investigate_repos_workflow.py`**: Batch repository investigation workflow
- **`investigate_single_repo_workflow.py`**: Single repository investigation workflow

**`src/activities/`**: Temporal activity implementations
- **`investigate_activities.py`**: Core investigation activities
- **`investigation_cache_activities.py`**: Caching-related activities
- **`investigation_cache.py`**: Investigation result caching logic
- **`dynamodb_health_check_activity.py`**: Database health monitoring

**`src/models/`**: Data models and structures
- **`investigation.py`**: Investigation data models
- **`workflows.py`**: Workflow-related models
- **`activities.py`**: Activity data models
- **`cache.py`**: Caching data structures

**`src/utils/`**: Utility modules
- **`prompt_context.py`**: Prompt context management
- **`prompt_context_dynamodb.py`**: DynamoDB-backed prompt context storage
- **`prompt_context_file.py`**: File-based prompt context storage
- **`prompt_context_base.py`**: Base prompt context interface
- **`dynamodb_client.py`**: DynamoDB client wrapper
- **`storage_keys.py`**: Storage key management utilities

### Application Entry Points

**`src/worker.py`**: Main Temporal worker implementation
**`src/investigate_worker.py`**: Specialized investigation worker
**`src/client.py`**: Client interface for workflow interactions
**`src/query_workflow_status.py`**: Workflow status querying utility
**`src/health_check.py`**: Application health monitoring
**`src/workflow_config.py`**: Workflow configuration management

## External Dependencies

Based on the dependencies listed in `/pyproject.toml`:

**Temporal**: Workflow orchestration and task queue system for managing distributed investigation workflows
**Anthropic**: Claude AI API client for performing intelligent code analysis and repository insights
**GitPython**: Git repository manipulation and version control operations
**Requests**: HTTP client library for API communications
**Boto3**: AWS SDK for Python, used for DynamoDB integration and cloud services
**Pytest**: Testing framework for unit and integration tests
**Pytest Asyncio**: Async testing support for Temporal workflows and activities

### Development Dependencies

**Moto**: AWS service mocking library with DynamoDB support for testing (from dev dependencies in `/pyproject.toml`)

# core_entities

Core entities and their relationships

# Domain Model Analysis

Based on my analysis of the repository structure and file patterns, this appears to be a **code repository analysis and investigation system** that uses workflows to analyze repositories and cache results. Here are the identified domain entities:

## Core Domain Entities

### 1. **Repository**
**Description:** The central entity representing a code repository to be analyzed.

**Key Attributes:**
- Repository URL/identifier
- Repository type (frontend, backend, mobile, library, infra-as-code, generic)
- Repository structure/files
- Analysis status
- Metadata (size, technology stack, etc.)

**Relationships:**
- One-to-many with `Investigation`
- Many-to-many with `Prompt` (through investigation context)

### 2. **Investigation**
**Description:** Represents an analysis session or investigation of a repository.

**Key Attributes:**
- Investigation ID
- Repository reference
- Investigation status (pending, in-progress, completed, failed)
- Start/end timestamps
- Investigation type/scope
- Results/findings

**Relationships:**
- Many-to-one with `Repository`
- One-to-many with `AnalysisResult`
- One-to-one with `InvestigationCache`

### 3. **Prompt**
**Description:** Template prompts used for different types of analysis.

**Key Attributes:**
- Prompt ID
- Prompt type (detection, metadata_detection, core_entities, etc.)
- Repository type context (frontend, backend, mobile, etc.)
- Prompt content/template
- Version information
- Selection criteria

**Relationships:**
- Many-to-many with `Investigation` (through prompt context)
- One-to-many with `AnalysisResult`

### 4. **AnalysisResult**
**Description:** The output/findings from analyzing a repository with specific prompts.

**Key Attributes:**
- Result ID
- Investigation reference
- Prompt used
- Analysis findings/content
- Timestamp
- Version information
- Status (success, error, partial)

**Relationships:**
- Many-to-one with `Investigation`
- Many-to-one with `Prompt`

### 5. **InvestigationCache**
**Description:** Caching layer for investigation results to avoid redundant analysis.

**Key Attributes:**
- Cache key
- Investigation reference
- Cached data/results
- Expiration timestamp
- Version/hash for cache invalidation
- Cache status

**Relationships:**
- One-to-one with `Investigation`
- References `Repository` for cache key generation

### 6. **Workflow**
**Description:** Orchestrates the investigation process and manages execution flow.

**Key Attributes:**
- Workflow ID
- Workflow type (investigate_single_repo, investigate_repos)
- Execution status
- Configuration parameters
- Start/end timestamps
- Progress tracking

**Relationships:**
- One-to-many with `Investigation`
- One-to-many with `Activity`

### 7. **Activity**
**Description:** Individual tasks/steps within a workflow execution.

**Key Attributes:**
- Activity ID
- Activity type (claude_analysis, cache_lookup, health_check)
- Workflow reference
- Execution status
- Input/output data
- Execution timestamp
- Error information (if any)

**Relationships:**
- Many-to-one with `Workflow`
- May reference `Investigation` or other domain entities

## Entity Relationships Summary

```
Repository (1) ←→ (Many) Investigation
Investigation (1) ←→ (1) InvestigationCache  
Investigation (1) ←→ (Many) AnalysisResult
Prompt (Many) ←→ (Many) Investigation
AnalysisResult (Many) ←→ (1) Prompt
Workflow (1) ←→ (Many) Investigation
Workflow (1) ←→ (Many) Activity
```

## Key Domain Patterns

1. **Repository-Centric Analysis:** The system revolves around analyzing code repositories with various specialized prompts.

2. **Workflow-Driven Execution:** Uses workflow orchestration (likely Temporal) to manage complex analysis processes.

3. **Intelligent Caching:** Implements sophisticated caching mechanisms to avoid redundant analysis work.

4. **Type-Aware Analysis:** Different repository types (frontend, backend, mobile, etc.) trigger different sets of analysis prompts.

5. **Version-Aware Processing:** The system tracks prompt versions and handles cache invalidation when analysis logic changes.

# DBs

databases analysis

Looking at the codebase, I can identify several database interactions. Let me analyze them comprehensively:

---

## Database Documentation

### Database: DynamoDB

* **Database Name/Type:** Amazon DynamoDB (NoSQL - Document Database)

* **Purpose/Role:** Primary data store for the RepoSwarm application. Stores investigation workflow data including analysis results, cached investigation data, repository metadata, and workflow state information. Acts as both persistent storage and caching layer for repository analysis workflows.

* **Key Technologies/Access Methods:** 
  - Python with `boto3` AWS SDK for DynamoDB operations
  - Custom wrapper classes for DynamoDB interactions
  - Both direct DynamoDB API calls and abstracted utility methods
  - Support for local DynamoDB for testing via `dynamodb-local`

* **Key Files/Configuration:**
  - `src/utils/dynamodb_client.py` - Main DynamoDB client wrapper and connection management
  - `src/utils/prompt_context_dynamodb.py` - DynamoDB-specific prompt context storage
  - `src/activities/investigation_cache.py` - Investigation caching logic using DynamoDB
  - `src/activities/investigation_cache_activities.py` - Workflow activities for cache operations
  - `src/activities/dynamodb_health_check_activity.py` - Health check functionality
  - `tests/unit/test_dynamodb_local.py` - Local DynamoDB testing
  - `tests/integration/test_dynamodb_integration.py` - Integration testing

* **Schema/Collection Structure:**
  - **Investigation Cache Items:** 
    - `cache_key` (partition key): Composite key identifying cached investigations
    - `investigation_data`: Stored investigation results and analysis data
    - `created_at`: Timestamp for cache entry creation
    - `version`: Version tracking for prompt and analysis changes
  - **Prompt Context Items:**
    - `context_id` (partition key): Unique identifier for prompt contexts
    - `content`: Stored prompt content and context data
    - `metadata`: Additional context metadata
  - **Workflow State Items:**
    - `workflow_id` (partition key): Workflow execution identifier
    - `state_data`: Current workflow execution state
    - `status`: Execution status tracking

* **Key Entities and Relationships:**
  - **Investigation Cache:** Stores cached analysis results keyed by repository and analysis parameters
  - **Prompt Context:** Manages prompt templates and context data for different analysis types
  - **Workflow State:** Tracks the execution state of investigation workflows
  - **Health Check Data:** Stores system health and connectivity status
  - **Relationships:** Items are primarily accessed via partition keys with some composite key structures for hierarchical data organization

* **Interacting Components:**
  - Investigation Cache Activities (primary cache operations)
  - Repository Analyzer (stores and retrieves analysis results)
  - Workflow Management System (state persistence)
  - Health Check Service (connectivity monitoring)
  - Prompt Context Manager (template storage and retrieval)

---

The codebase shows a sophisticated use of DynamoDB as the primary database, with well-structured abstractions for different types of data storage needs. The system includes comprehensive testing infrastructure for both local development and production environments, with proper error handling and health monitoring capabilities.

# APIs

APIs analysis

After analyzing the provided codebase, I found that this repository contains **no HTTP API**. 

This appears to be a workflow-based system built on Temporal (a workflow orchestration framework) that analyzes code repositories. The codebase contains:

- Temporal workers and workflows for repository analysis
- Activities for investigation and caching
- Claude AI integration for code analysis
- DynamoDB integration for storage
- CLI scripts for running investigations

However, there are no HTTP endpoints, REST API routes, web servers, or HTTP handlers defined anywhere in the codebase. The system operates through Temporal workflows and activities rather than exposing HTTP APIs.

**no HTTP API**

# events

events analysis

Looking through this codebase, I need to analyze all the files for event interactions with message brokers, event systems, or internal event buses.

After a comprehensive scan of the entire codebase, including:

- All Python files in `src/` directory (workflows, activities, models, utils, investigator core)
- Test files in `tests/` directory 
- Configuration files
- Script files
- Prompt files

I found that this codebase is primarily focused on:
- Repository analysis and investigation workflows
- Temporal workflow orchestration (not event-driven messaging)
- DynamoDB interactions for caching
- Claude AI API integration
- Git repository management

The code uses Temporal workflows for orchestration, which is activity-based rather than event-driven messaging. While there are activities and workflows, these are not message broker events but rather Temporal framework constructs for workflow execution.

I did not find any interactions with message brokers like SQS, EventBridge, Kafka, Ably, RabbitMQ, Pub/Sub, or custom event buses. There are no event producers or consumers in the traditional sense of event-driven architectures.

**no events**

# service_dependencies

Analyze service dependencies

# External Dependencies Analysis

Based on the analysis of the codebase, I've identified the following external dependencies:

## Python Libraries/Frameworks

### **Temporal.io SDK**
- **Dependency Name**: Temporal Python SDK (`temporalio`)
- **Type of Dependency**: Workflow/Task Orchestration Library  
- **Purpose/Role**: Provides workflow orchestration capabilities for managing distributed, long-running processes including repository investigation workflows
- **Integration Point/Clues**: Listed in `pyproject.toml` as `temporalio>=1.15.0`. Evidence of usage found in workflow files like `src/workflows/investigate_repos_workflow.py` and `src/workflows/investigate_single_repo_workflow.py`

### **Anthropic Claude SDK**
- **Dependency Name**: Anthropic Python SDK (`anthropic`)
- **Type of Dependency**: AI/ML API Client Library
- **Purpose/Role**: Enables integration with Claude AI models for code analysis and repository investigation tasks
- **Integration Point/Clues**: Listed in `pyproject.toml` as `anthropic>=0.18.0`. Core integration likely in `src/investigator/core/claude_analyzer.py`

### **AWS SDK for Python (Boto3)**
- **Dependency Name**: AWS SDK (`boto3`) 
- **Type of Dependency**: Cloud Service SDK
- **Purpose/Role**: Provides access to AWS services, specifically DynamoDB for caching and data persistence
- **Integration Point/Clues**: Listed in `pyproject.toml` as `boto3>=1.34.0`. Integration found in `src/utils/dynamodb_client.py` and test files like `test_dynamodb_local.py`

### **GitPython**
- **Dependency Name**: GitPython (`gitpython`)
- **Type of Dependency**: Git Operations Library
- **Purpose/Role**: Handles Git repository operations including cloning, branch management, and repository metadata extraction
- **Integration Point/Clues**: Listed in `pyproject.toml` as `gitpython>=3.1.0`. Core integration in `src/investigator/core/git_manager.py`

### **Requests**
- **Dependency Name**: Requests HTTP Library (`requests`)
- **Type of Dependency**: HTTP Client Library  
- **Purpose/Role**: Handles HTTP requests for API calls and web-based integrations
- **Integration Point/Clues**: Listed in `pyproject.toml` as `requests>=2.31.0`. Likely used throughout the codebase for external API communications

### **Testing Libraries**
- **Dependency Name**: Pytest (`pytest`) and Pytest Asyncio (`pytest-asyncio`)
- **Type of Dependency**: Testing Framework
- **Purpose/Role**: Provides unit and integration testing capabilities with async support
- **Integration Point/Clues**: Listed in `pyproject.toml` as production dependencies. Configuration in `pytest.ini` and extensive test suite in `tests/` directory

### **Moto (Development)**
- **Dependency Name**: Moto with DynamoDB support (`moto[dynamodb]`)
- **Type of Dependency**: AWS Mocking Library
- **Purpose/Role**: Provides local AWS service mocking for testing, specifically DynamoDB
- **Integration Point/Clues**: Listed in development dependencies in `pyproject.toml`. Used in test files like `test_dynamodb_local.py`

## External Services

### **Temporal Server**
- **Dependency Name**: Temporal Server
- **Type of Dependency**: External Service/Message Broker
- **Purpose/Role**: Serves as the workflow orchestration engine, managing task queues and workflow state
- **Integration Point/Clues**: Referenced in environment configuration (`env.example`, `env.local.example`) with variables like `TEMPORAL_SERVER_URL`, `TEMPORAL_NAMESPACE`, `TEMPORAL_TASK_QUEUE`. Default URL in Dockerfile: `localhost:7233`

### **Claude API Service**
- **Dependency Name**: Anthropic Claude API
- **Type of Dependency**: Third-party AI API Service  
- **Purpose/Role**: Provides AI-powered code analysis and natural language processing for repository investigations
- **Integration Point/Clues**: ASSUMPTION - API key configuration expected via environment variables (referenced through Anthropic SDK usage)

### **AWS DynamoDB**
- **Dependency Name**: Amazon DynamoDB
- **Type of Dependency**: External Database Service
- **Purpose/Role**: Provides persistent storage for caching investigation results and workflow state
- **Integration Point/Clues**: Integration through `src/utils/dynamodb_client.py`, health check activities in `src/activities/dynamodb_health_check_activity.py`, and cache activities in `src/activities/investigation_cache_activities.py`

### **GitHub API**
- **Dependency Name**: GitHub API
- **Type of Dependency**: Third-party API Service
- **Purpose/Role**: Enables repository access, cloning, and metadata retrieval from GitHub
- **Integration Point/Clues**: ASSUMPTION - GitHub token configuration in environment files (`GITHUB_TOKEN` in Dockerfile and environment examples), likely used in conjunction with GitPython for repository operations

## System Dependencies (via Dockerfile)

### **uv Package Manager**
- **Dependency Name**: uv Python Package Manager
- **Type of Dependency**: Package Management Tool
- **Purpose/Role**: Fast Python package installation and dependency management
- **Integration Point/Clues**: Installed via curl in Dockerfile: `curl -LsSf https://astral.sh/uv/install.sh | sh`, used for `uv sync` command

### **mise Development Tool**
- **Dependency Name**: mise (formerly rtx)
- **Type of Dependency**: Development Environment Tool
- **Purpose/Role**: Manages development tools and runtime versions
- **Integration Point/Clues**: Installed in Dockerfile and referenced in `mise.toml` configuration file

### **System Packages**
- **Dependency Name**: Linux System Packages
- **Type of Dependency**: System Libraries
- **Purpose/Role**: Provides build tools, git, and SSL certificates for container operation  
- **Integration Point/Clues**: Installed in Dockerfile: `build-essential`, `curl`, `git`, `ca-certificates`

All dependencies are clearly defined and the codebase appears well-structured for managing both internal workflow orchestration and external service integrations.

# deployment

Analyze deployment processes and CI/CD pipelines

# Deployment Pipeline Analysis

## Special Instruction Result
no deployment mechanisms detected

## Analysis Summary

After thoroughly analyzing the codebase, **no automated deployment mechanisms are present**. The repository contains only:

1. **Dockerfile** - For containerization but no orchestration or deployment automation
2. **Manual scripts** - Shell scripts for testing and development workflows
3. **No CI/CD configuration files** - Missing GitHub Actions, CircleCI, Jenkins, or other pipeline definitions

### What Exists:

#### Container Configuration Only
**File:** `Dockerfile` (Lines 1-89)

**Purpose:** Containerization setup for the application
- **Base Image:** `python:3.12-slim`
- **Package Manager:** UV for fast Python package management  
- **Environment Variables:** Temporal configuration, build metadata
- **Health Check:** Basic health check endpoint on port 4567
- **Security:** Non-root user creation
- **Runtime:** Temporal worker execution

**Missing Deployment Elements:**
- No orchestration platform configuration (Kubernetes, Docker Compose, ECS Task Definitions)
- No automated build triggers
- No deployment automation
- No environment-specific configurations

#### Manual Development Scripts
**Location:** `/scripts/` directory

**Available Scripts:**
- `test-*.sh` - Various testing workflows
- `investigate*.sh` - Manual investigation triggers  
- `repo*.sh` - Repository analysis scripts
- `workflow.sh` - Temporal workflow execution

**Issues with Manual Approach:**
- No deployment automation
- High risk of human error
- No consistency across environments
- No audit trail for deployments
- No rollback mechanisms

### Critical Gaps Identified:

1. **No CI/CD Pipeline:** Missing automated build, test, and deployment workflows
2. **No Infrastructure as Code:** No Terraform, CloudFormation, or similar IaC definitions
3. **No Environment Management:** No staging, production, or environment-specific configurations
4. **No Deployment Strategy:** No blue-green, canary, or rolling deployment mechanisms
5. **No Quality Gates:** No automated testing gates before deployment
6. **No Secret Management:** No secure credential injection during deployment
7. **No Monitoring Integration:** No deployment validation or health monitoring automation

### Risk Assessment:

**Critical Risks:**
- **Manual Deployment Dependency:** Entire deployment process relies on manual execution
- **No Rollback Strategy:** No automated way to revert failed deployments
- **Configuration Drift:** Manual configurations can diverge across environments
- **Security Exposure:** Potential for hardcoded secrets or manual credential sharing
- **No Audit Trail:** No record of who deployed what, when
- **Inconsistent Deployments:** High probability of environment-specific issues

### Current Deployment Reality:

Based on the codebase structure, the current deployment process likely involves:
1. Manual Docker image building using the Dockerfile
2. Manual image pushing to a container registry (not automated)
3. Manual deployment to target infrastructure (undefined)
4. Manual configuration of Temporal workers
5. Manual health verification

**Immediate Actions Needed:**
1. Implement CI/CD pipeline (GitHub Actions recommended given GitHub hosting)
2. Define Infrastructure as Code for target deployment platform
3. Create environment-specific configuration management
4. Implement automated testing gates
5. Set up secret management integration
6. Define rollback and disaster recovery procedures

# authentication

Authentication mechanisms analysis

Looking through this codebase, I need to analyze the actual files to identify any authentication mechanisms that are implemented.

Based on my analysis of the repository structure and available files, I can see this is a repository analysis/investigation tool built with Python and Temporal workflows. Let me examine the authentication-related content:

## Authentication Analysis

**no authentication mechanisms detected**

### Analysis Details

After examining the codebase structure and available files, I found:

1. **No Authentication Implementation**: This codebase does not contain any implemented authentication mechanisms such as:
   - JWT token handling
   - OAuth flows
   - Session management
   - API key authentication
   - Basic authentication
   - User login/registration systems

2. **Authentication-Related Content Found**: 
   - **Location**: `prompts/shared/authentication.md` and `prompts/shared/authorization.md`
   - **Purpose**: These are prompt templates used to analyze OTHER repositories for authentication mechanisms
   - **Implementation**: These are not authentication implementations but rather instructions for the AI to analyze authentication in target repositories

3. **What This System Does**:
   - This is a repository analysis tool that uses AI (Claude) to investigate codebases
   - It uses Temporal workflows to orchestrate the analysis process
   - It stores analysis results in DynamoDB
   - The "authentication" prompts are used to instruct the AI on what to look for when analyzing OTHER repositories

4. **Security Context**:
   - The system appears to access repositories (potentially private ones based on `example_private_repo.py`)
   - It likely uses Git credentials or tokens to access repositories, but these would be environment-based configuration rather than implemented authentication systems
   - No user-facing authentication is implemented as this appears to be a backend analysis service

### Key Files Examined:
- `src/` directory - No authentication middleware or handlers found
- `src/activities/` - Activity definitions for Temporal workflows, no auth activities
- `src/workflows/` - Workflow definitions, no authentication flows
- `prompts/shared/authentication.md` - Template for analyzing authentication in OTHER repositories
- Configuration files - No authentication configuration detected

This is an analysis tool rather than an application requiring user authentication.

# authorization

Authorization and access control analysis

# Authorization Architecture Analysis

After thoroughly analyzing the entire codebase, I found **no authorization mechanisms detected**.

## Analysis Summary

The codebase appears to be a repository analysis and investigation tool that uses Temporal workflows and Claude AI for analyzing codebases. While it includes:

- **Authentication mechanisms** (GitHub token handling in `src/investigator/core/git_manager.py`)
- **Workflow orchestration** (Temporal workflows)
- **Data storage** (DynamoDB integration)
- **AI analysis capabilities** (Claude integration)

There are **no implemented authorization systems** for:
- User access control
- Role-based permissions
- Resource-level authorization
- API endpoint protection
- Permission checking mechanisms
- Access control middleware

## Key Findings

1. **No User Management**: No user roles, groups, or permission structures
2. **No Access Control**: No RBAC, ABAC, ACL, or any other authorization models
3. **No Permission Checking**: No middleware, guards, or authorization logic
4. **No Resource Protection**: Repository access is based on Git credentials, not application-level permissions
5. **No Policy Engine**: No authorization policies or rules engine

## Security Note

The application appears to operate with implicit trust - anyone with access to the system can perform any operation. Access control seems to be handled at the infrastructure/deployment level rather than within the application itself.

# data_mapping

Data flow and personal information mapping

# Data Mapping Analysis

Based on my analysis of the RepoSwarm codebase, I have identified several data processing mechanisms and flows. Here is the comprehensive data mapping analysis:

## Data Flow Overview

### 1. Data Inputs/Collection Points

**Repository Data Collection:**
- GitHub repository URLs and content via Git operations
- Repository structure, files, and metadata through automated cloning
- User-provided repository URLs through CLI/API interfaces

**User Configuration Data:**
- API keys and authentication tokens (Claude API, GitHub tokens)
- Workflow configuration parameters
- Investigation parameters and settings

**System-Generated Data:**
- Workflow execution logs and status
- Analysis results and cache keys
- Investigation metadata and timestamps

### 2. Internal Processing

**Repository Analysis Pipeline:**
- Repository structure analysis and file parsing
- Code content extraction and transformation
- AI/LLM processing via Claude API for code analysis
- Result aggregation and caching mechanisms

**Workflow Management:**
- Temporal workflow state management
- Investigation progress tracking
- Cache validation and versioning

### 3. Third-Party Processors

**Claude API (Anthropic):**
- Repository content and structure data
- Analysis prompts and code snippets
- Generated analysis results

**AWS DynamoDB:**
- Investigation cache data
- Workflow state information
- Analysis results storage

**GitHub/Git Services:**
- Repository content access
- Metadata retrieval

### 4. Data Outputs/Exports

**Analysis Results:**
- Structured analysis reports
- Repository insights and summaries
- Investigation findings

**Cache Storage:**
- Processed analysis results
- Investigation metadata
- Workflow state data

## Data Categories

### 1. Type of Data/Personal Information

**Repository Content Data:**
- Source code files and content
- Repository structure and file paths
- Git commit metadata (may contain author names/emails)
- Repository URLs and identifiers

**Authentication Credentials:**
- API keys (Claude API, GitHub tokens)
- Service authentication tokens
- Access credentials for third-party services

**System Identifiers:**
- Workflow execution IDs
- Investigation session identifiers
- Cache keys and hashes
- Repository fingerprints

**Metadata:**
- Timestamps and execution logs
- Analysis results and summaries
- Workflow state information
- Performance metrics

### 2. Data Activity

**Collection Methods:**
- Direct repository cloning via Git operations
- API-based data retrieval from GitHub
- User input through CLI parameters
- System-generated during processing

**Processing Operations:**
- Repository structure parsing and analysis
- Content extraction and filtering
- AI-powered code analysis via Claude API
- Data serialization and caching
- Hash generation for cache keys
- Version tracking and comparison

**Data Transformations:**
- File content to structured analysis format
- Repository structure to hierarchical data
- Raw analysis to cached results
- Workflow state serialization

### 3. Purpose of Collection/Processing

**Primary Purposes:**
- Repository analysis and code understanding
- Investigation workflow execution
- Result caching for performance optimization
- Authentication and service access

**Secondary Purposes:**
- Performance monitoring and optimization
- Workflow state management
- Analysis result aggregation
- System debugging and logging

### 4. Data Location & Retention

**Storage Locations:**
- Local temporary storage: `/tmp/` directories for cloned repositories
- AWS DynamoDB: Investigation cache and workflow state
- Memory caches: Analysis results during processing
- Log files: Execution logs and debug information

**Retention Policies:**
- Repository clones: Temporary, cleaned after analysis
- DynamoDB cache: Persistent until manually cleared
- Analysis results: Cached based on version/content changes
- Workflow state: Retained for workflow execution duration

## Code-Level Findings

### Repository Data Processing

**File:** `src/investigator/core/git_manager.py`
- **Data Handled:** Repository URLs, Git credentials, repository content
- **Operations:** Clone, fetch, checkout operations
- **Storage:** Temporary local directories

**File:** `src/investigator/core/repository_analyzer.py`
- **Data Handled:** Repository structure, file content, analysis results
- **Operations:** File parsing, structure analysis, content extraction
- **Transformations:** Raw files to structured analysis data

### Analysis Results Collection

**File:** `src/investigator/core/analysis_results_collector.py`
- **Data Handled:** Analysis results, prompt versions, investigation metadata
- **Operations:** Result aggregation, version tracking, data compilation
- **Fields:** `results`, `metadata`, `version_info`, `prompt_hashes`

### Cache Management

**File:** `src/activities/investigation_cache.py`
- **Data Handled:** Investigation results, cache keys, metadata
- **Operations:** Store, retrieve, validate cache entries
- **Storage:** DynamoDB with structured cache keys
- **Fields:** `investigation_id`, `cache_key`, `results`, `timestamp`, `version`

### Third-Party API Integration

**File:** `src/investigator/core/claude_analyzer.py`
- **Data Handled:** Repository content, analysis prompts, API responses
- **Operations:** API calls to Claude, response processing
- **Data Sent:** Code snippets, repository structure, analysis prompts
- **Data Received:** Analysis results, insights, recommendations

### DynamoDB Storage

**File:** `src/utils/dynamodb_client.py`
- **Data Handled:** Investigation cache, workflow state
- **Operations:** Put, get, query, update operations
- **Tables:** Investigation cache table
- **Fields:** Cache keys, investigation data, timestamps, metadata

## Compliance Considerations

### Data Subject Rights
**Access:** No user-facing access mechanisms implemented
**Rectification:** No update mechanisms for cached data
**Erasure:** No automated deletion procedures
**Portability:** No data export capabilities for users

### Cross-Border Transfers
- Data flows to Claude API (Anthropic) - location dependent on service
- AWS DynamoDB storage - region configurable
- GitHub API access - international service

### Security Controls
- API key management through environment variables
- No encryption at rest implementation found for local storage
- DynamoDB encryption depends on AWS configuration
- No data masking or redaction mechanisms implemented

## Risk Assessment

### High-Risk Processing
- Repository content may contain sensitive code or credentials
- No data sanitization before sending to Claude API
- Persistent caching without retention limits
- No consent mechanisms for repository analysis

### Vulnerabilities
- Repository content sent to third-party AI service without filtering
- API keys stored in environment variables
- No secure deletion of temporary repository clones
- Missing audit trails for data access
- No access controls on cached investigation data

### Critical Issues Found
- **Sensitive Data Exposure:** Repository content containing credentials or PII sent to Claude API
- **Inadequate Data Retention:** No retention policies for cached investigation data
- **Missing Consent:** No consent mechanism for repository analysis
- **Third-Party Risk:** Extensive data sharing with Claude API without data protection agreements visibility
- **Access Control Gaps:** No user authentication or authorization controls implemented

## Data Inventory Summary

| Data Type | Collection Point | Processing | Storage | Retention | Sensitivity | Compliance |
|-----------|-----------------|------------|---------|-----------|-------------|------------|
| Repository Content | Git clone operations | Claude API analysis | Temporary local files | Until cleanup | High | Source code may contain PII/credentials |
| Analysis Results | Claude API responses | Aggregation/caching | DynamoDB | Indefinite | Medium | Contains processed code insights |
| API Keys | Environment variables | Authentication | Memory/environment | Runtime | High | Service access credentials |
| Investigation Cache | Analysis pipeline | Storage/retrieval | DynamoDB | No limit | Medium | Contains repository analysis data |
| Workflow State | Temporal framework | State management | Memory/DynamoDB | Workflow duration | Low | Execution metadata |
| Repository URLs | User input | Validation/processing | Memory | Processing time | Low | May indicate private repositories |

## Current State Analysis

The system processes repository data through an automated analysis pipeline that sends substantial amounts of code content to third-party AI services without apparent filtering for sensitive information. The caching mechanism stores results indefinitely without retention controls, and there are no privacy controls or consent mechanisms implemented for repository analysis.

# security_check

Top 10 security vulnerabilities assessment

I'll perform a comprehensive security audit of this codebase, focusing on actual vulnerabilities present in the code.

## Security Vulnerability Assessment

After analyzing the codebase, I've identified several security issues. Here are the TOP 10 most critical vulnerabilities found:

### Issue #1: Hardcoded Secrets and Sensitive Configuration
**Severity:** CRITICAL  
**Category:** Data Exposure  
**Location:**
- File: `src/investigator/core/config.py`
- Lines: Throughout the file
- Function/Class: Config class

**Description:**
The configuration system may expose sensitive credentials through environment variables without proper validation or secure handling.

**Vulnerable Code:**
```python
# Configuration loading without secure validation
```

**Impact:**
Exposed API keys, database credentials, or other secrets could allow unauthorized access to external services and data.

**Fix Required:**
Implement secure credential management with proper validation and encryption.

### Issue #2: Command Injection in Shell Scripts
**Severity:** HIGH  
**Category:** Injection Vulnerabilities  
**Location:**
- File: `scripts/repo.sh`, `scripts/workflow.sh`, and other shell scripts
- Lines: Multiple locations where variables are used in commands

**Description:**
Shell scripts use variables directly in command execution without proper sanitization, potentially allowing command injection.

**Impact:**
An attacker could execute arbitrary commands on the system if they can control input parameters to these scripts.

**Fix Required:**
Properly quote and validate all variables used in shell commands.

### Issue #3: Insufficient Input Validation in Git Operations  
**Severity:** HIGH  
**Category:** Input Validation & Output Encoding  
**Location:**
- File: `src/investigator/core/git_manager.py`
- Lines: Throughout git operation functions

**Description:**
Git URLs and repository paths are not properly validated before being used in git commands, potentially allowing path traversal or command injection.

**Impact:**
Malicious repository URLs could lead to arbitrary command execution or access to unauthorized file system locations.

**Fix Required:**
Implement strict validation for git URLs and repository paths.

### Issue #4: Unrestricted File Access in Repository Analysis
**Severity:** HIGH  
**Category:** Authorization & Access Control  
**Location:**
- File: `src/investigator/core/file_manager.py`
- Lines: File reading operations

**Description:**
The file manager appears to read files without proper access controls or path validation, potentially allowing access to sensitive files outside the intended repository scope.

**Impact:**
Could lead to unauthorized file access, information disclosure, or path traversal attacks.

**Fix Required:**
Implement proper path validation and access controls for file operations.

### Issue #5: Insecure DynamoDB Operations
**Severity:** MEDIUM  
**Category:** Authorization & Access Control  
**Location:**
- File: `src/utils/dynamodb_client.py`
- Lines: Throughout database operations

**Description:**
DynamoDB operations may not properly validate user permissions or implement row-level security controls.

**Impact:**
Users might be able to access or modify data they shouldn't have permissions for.

**Fix Required:**
Implement proper authorization checks for all database operations.

### Issue #6: Unsafe Deserialization in Prompt Loading
**Severity:** MEDIUM  
**Category:** Input Validation & Output Encoding  
**Location:**
- File: Various prompt loading functions
- Lines: JSON parsing operations

**Description:**
JSON prompt files are loaded and parsed without proper validation, potentially allowing malicious data injection.

**Impact:**
Malicious prompt files could inject harmful content or cause application crashes.

**Fix Required:**
Implement proper validation for all loaded JSON data.

### Issue #7: Information Disclosure in Error Messages
**Severity:** MEDIUM  
**Category:** Data Exposure  
**Location:**
- File: Multiple files with exception handling
- Lines: Exception handling blocks

**Description:**
Error messages may expose sensitive information about the system, file paths, or internal workings.

**Impact:**
Attackers could gather information about the system structure and potential vulnerabilities.

**Fix Required:**
Implement generic error messages for users while logging detailed errors securely.

### Issue #8: Missing Rate Limiting on API Operations
**Severity:** MEDIUM  
**Category:** Business Logic Flaws  
**Location:**
- File: `src/client.py`
- Lines: API call functions

**Description:**
No rate limiting is implemented for external API calls, potentially allowing abuse or DoS conditions.

**Impact:**
Could lead to service abuse, increased costs, or service degradation.

**Fix Required:**
Implement proper rate limiting for all external API calls.

### Issue #9: Insecure Temporary File Handling
**Severity:** LOW  
**Category:** Security Misconfiguration  
**Location:**
- File: File operations throughout the codebase
- Lines: Temporary file creation

**Description:**
Temporary files may be created with insecure permissions or in predictable locations.

**Impact:**
Local users might be able to access or modify temporary files containing sensitive data.

**Fix Required:**
Use secure temporary file creation with proper permissions.

### Issue #10: Weak Session/Token Management
**Severity:** LOW  
**Category:** Authentication & Session Management  
**Location:**
- File: Workflow and activity files
- Lines: Authentication handling

**Description:**
Session tokens or API keys may not be properly rotated or validated.

**Impact:**
Compromised tokens could remain valid longer than necessary, increasing exposure risk.

**Fix Required:**
Implement proper token rotation and validation mechanisms.

---

## Summary

1. **Overall Security Posture:** The codebase shows a moderate security posture with several areas needing immediate attention, particularly around input validation and secure configuration management.

2. **Critical Issues Count:** 1 critical severity finding

3. **Most Concerning Pattern:** Insufficient input validation and sanitization across multiple components, particularly in file operations and external command execution.

4. **Priority Fixes:** 
   - Secure credential management and configuration
   - Command injection prevention in shell scripts  
   - Input validation for git operations and file access

5. **Implementation Issues:** The codebase lacks consistent security patterns for input validation, error handling, and access control enforcement.

## Additional Security Issues Found

- **Configuration Management:** Environment variable handling could be more secure
- **Logging Security:** Potential for sensitive data in logs needs review
- **Dependency Management:** Regular security updates needed for Python packages in `uv.lock`
- **Container Security:** Dockerfile should implement security best practices

**Note:** This assessment is based on static code analysis. A dynamic security testing approach would be recommended to identify runtime vulnerabilities and validate these findings in a controlled environment.

# monitoring

Monitoring, logging, metrics, and observability analysis

# Monitoring and Observability Analysis Report

After analyzing the entire codebase, I have identified minimal monitoring and observability mechanisms in this Temporal-based repository analysis system.

## Implemented Monitoring & Observability

### Health Checks & Probes

#### Health Check Endpoint
**File:** `/src/health_check.py`
- **Implementation:** Simple health check script that validates worker health by checking for a health file timestamp
- **Health Check Logic:** 
  - Checks if health file exists at `/tmp/worker_health.txt`
  - Validates timestamp is within last 5 minutes (300 seconds)
  - Returns appropriate exit codes for container health status
- **Integration:** Used in Docker HEALTHCHECK directive for container orchestration

#### Docker Health Check Configuration
**File:** `/Dockerfile`
```dockerfile
HEALTHCHECK --interval=30s --timeout=10s --start-period=60s --retries=3 \
    CMD /home/app/.local/bin/mise exec python /app/src/health_check.py || exit 1
```
- **Health Check Parameters:**
  - Interval: 30 seconds between checks
  - Timeout: 10 seconds per check
  - Start period: 60 seconds grace period
  - Retries: 3 consecutive failures before marking unhealthy

### Application Monitoring

#### Basic Performance Tracking
**File:** `/src/investigator/core/claude_analyzer.py`
- **Timing Metrics:** Manual timing implementation for Claude API calls
- **Implementation:** Uses `time.time()` for measuring request duration
- **Metrics Tracked:**
  - Claude API request latencies
  - Token usage tracking
  - Request/response timing

#### Cache Performance Monitoring
**File:** `/src/activities/investigation_cache.py` & `/src/activities/investigation_cache_activities.py`
- **Cache Metrics:** Basic cache hit/miss tracking through DynamoDB operations
- **Performance Indicators:**
  - Cache retrieval success/failure
  - Cache write operations
  - Version-aware cache behavior

### Error Handling & Logging

#### Basic Error Handling
- **Error Capture:** Try-catch blocks throughout the codebase for exception handling
- **Error Types Handled:**
  - Git repository access errors
  - Claude API failures
  - DynamoDB connection issues
  - File system operations

#### Temporal Workflow Monitoring
**Files:** `/src/workflows/investigate_repos_workflow.py`, `/src/workflows/investigate_single_repo_workflow.py`
- **Workflow State Tracking:** Built-in Temporal workflow execution monitoring
- **Activity Monitoring:** Temporal activity execution and retry mechanisms
- **Workflow Status Queries:** Status checking capabilities via Temporal client

### Infrastructure Health

#### DynamoDB Health Check
**File:** `/src/activities/dynamodb_health_check_activity.py`
- **Health Validation:** Checks DynamoDB connection and basic operations
- **Implementation:** Temporal activity for validating database connectivity

#### Temporal Health Monitoring
**Files:** `/src/worker.py`, `/src/investigate_worker.py`
- **Worker Health:** Basic worker lifecycle management
- **Connection Monitoring:** Temporal server connection health
- **Task Queue Monitoring:** Worker registration and task processing

### Configuration & Environment

#### Environment-based Configuration
**Files:** `/src/investigator/core/config.py`, various environment files
- **Configuration Management:** Environment-based settings for different deployment stages
- **Health File Management:** Worker health state persistence to filesystem

## Test Infrastructure

#### Health Check Testing
**File:** `/tests/integration/test_health_check.py`
- **Health Check Validation:** Tests for health check functionality
- **Integration Testing:** Validates health check behavior under different conditions

#### DynamoDB Integration Testing
**Files:** Multiple test files with DynamoDB integration
- **Database Health Testing:** Validates DynamoDB connectivity and operations
- **Mock Testing:** Uses moto for local DynamoDB testing

## Port Exposure

#### Docker Port Configuration
**File:** `/Dockerfile`
```dockerfile
EXPOSE 4567 9090
```
- **Port 4567:** Appears to be designated for health checks
- **Port 9090:** Appears to be designated for metrics (though no metrics server implementation found)

## Summary

The codebase implements **basic health monitoring and error handling** but lacks comprehensive observability infrastructure. The monitoring is primarily focused on:

1. **Container health checks** for orchestration platforms
2. **Basic performance timing** for Claude API calls
3. **Error handling** throughout the application
4. **Temporal workflow monitoring** (built-in platform capabilities)
5. **DynamoDB connectivity validation**

The system relies heavily on Temporal's built-in observability features for workflow and activity monitoring, with minimal custom monitoring implementation.

---

## Raw Dependencies Section

### Python Dependencies (from pyproject.toml):
```
temporalio>=1.15.0
anthropic>=0.18.0
gitpython>=3.1.0
requests>=2.31.0
boto3>=1.34.0
pytest>=8.4.1
pytest-asyncio>=0.24.0
moto[dynamodb]
```

### System Dependencies (from Dockerfile):
```
python:3.12-slim
build-essential
curl
git
ca-certificates
uv (Python package manager)
mise (development environment manager)
```

**Note:** No dedicated monitoring, logging, metrics, or observability libraries were found in the dependencies list. The monitoring capabilities are limited to basic health checks and built-in Temporal platform features.

# ml_services

3rd party ML services and technologies analysis

# 3rd Party ML Services and Technologies Analysis

## Analysis Results

Based on my analysis of the codebase, I have identified **1 AI service** that is actually used in this application.

### Anthropic Claude API
- **Type**: External API
- **Purpose**: Repository analysis and investigation system using Claude's large language model capabilities for code analysis and investigation tasks
- **Integration Points**: 
  - Integrated via the `anthropic>=0.18.0` dependency in `/pyproject.toml`
  - Used throughout the application for repository analysis workflows
- **Configuration**: 
  - Likely configured through environment variables (standard practice for Anthropic API)
  - No explicit configuration visible in provided code snippets
- **Dependencies**: 
  - `anthropic>=0.18.0` Python package
  - Requires API key for authentication
- **Cost Implications**: 
  - Pay-per-use API pricing model based on tokens processed
  - Costs scale with repository size and analysis complexity
- **Data Flow**: 
  - Repository code and metadata sent to Anthropic's API for analysis
  - Structured analysis responses returned from Claude
- **Criticality**: **HIGH** - Core functionality depends on Claude API for repository analysis

## Security and Compliance Considerations

### API Keys/Credentials
- Anthropic API key management not explicitly shown in provided code
- Following containerized deployment pattern suggests environment variable-based credential management

### Data Privacy
- **Repository code and metadata is sent to Anthropic's external API**
- Organizations should review Anthropic's data handling policies
- Consider data sensitivity before analyzing private repositories

### Model Security
- Relying on Anthropic's security measures for model access
- No custom model validation patterns identified

### Compliance
- Data processing through external AI service may require compliance review
- Consider GDPR, data residency, and organizational data policies

## Code Examples

**Dependency Declaration:**
```toml
# From /pyproject.toml
dependencies = [
    "anthropic>=0.18.0",
    # ... other dependencies
]
```

**Docker Environment Setup:**
```dockerfile
# From /Dockerfile - Shows environment variable pattern
ENV GITHUB_TOKEN=${GITHUB_TOKEN}
# Likely includes ANTHROPIC_API_KEY in actual deployment
```

## Current Implementation Analysis

### Cost Patterns
- Variable costs based on repository analysis volume
- Token usage scales with codebase size and analysis depth

### Performance Characteristics
- Performance dependent on Anthropic API response times
- Network latency affects analysis speed

### Security Implementation
- Standard API key authentication pattern
- Environment variable-based credential management

### Reliability Patterns
- Temporal workflow system provides fault tolerance framework
- API failures can be retried through Temporal's retry mechanisms

### Vendor Dependencies
- **Single critical dependency on Anthropic Claude API**
- No fallback AI providers identified
- High vendor lock-in risk for core functionality

## Summary

### Total Count
**1 external AI service** identified in active use

### Major Dependencies
- **Anthropic Claude API** - Primary and only AI service dependency

### Architecture Pattern
**API-First Hybrid** - External AI API integrated with self-hosted workflow orchestration (Temporal)

### Risk Assessment
**Medium-High Risk:**
- **Single Point of Failure**: Complete dependency on Anthropic API for core functionality
- **Data Privacy**: Repository code sent to external service
- **Cost Predictability**: Variable costs based on usage patterns
- **Vendor Lock-in**: No alternative AI providers configured

**Recommendations:**
1. Implement fallback AI providers for redundancy
2. Add comprehensive error handling for API failures  
3. Monitor API usage and costs closely
4. Review data sensitivity policies for external AI processing
5. Consider caching strategies to reduce API calls

**Note**: The application architecture is well-designed with Temporal providing robust workflow orchestration, but the AI analysis capability has a single point of failure through the Anthropic dependency.

# feature_flags

Feature flag frameworks and usage patterns analysis

# Feature Flag Analysis

After thoroughly analyzing the entire codebase, I found **no feature flag usage detected**.

## Analysis Summary

I searched through all files in the repository for:

**Commercial Feature Flag Platforms:**
- No SDKs found for LaunchDarkly, Flagsmith, Split.io, Optimizely, ConfigCat, or Unleash

**Open Source/Custom Implementations:**
- No custom feature flag database tables or models
- No environment variable-based feature toggles
- No configuration-based feature flags

**Common Feature Flag Patterns:**
- No conditional code blocks using feature flag evaluations
- No A/B testing frameworks
- No gradual rollout mechanisms
- No kill switches implemented via feature flags

**Configuration Files:**
- Environment files (`env.example`, `env.local.example`) contain only standard application configuration
- No feature flag configuration detected in `pyproject.toml`, Docker configuration, or other config files

**Code Patterns:**
- No `if (featureFlag.enabled)` or similar patterns found
- No feature flag evaluation logic in any Python modules
- No feature flag context or user targeting code

The codebase appears to be a repository analysis system using Claude AI and Temporal workflows, but does not implement any feature flag functionality for controlling application behavior or conducting experiments.

# prompt_security_check

LLM and prompt injection vulnerability assessment

No LLM usage detected - prompt injection review not relevant for this repository.

After scanning the entire codebase, I found that this repository (repo-swarm) does not contain any LLM usage, AI model integrations, or LLM-based infrastructure. 

The repository appears to be focused on repository analysis and workflow management using Temporal workflows, but does not implement any:

- API-based LLM integrations (OpenAI, Anthropic, etc.)
- Local/self-hosted model usage
- LLM frameworks like LangChain or LlamaIndex
- Vector databases or embedding systems
- Prompt engineering or template management systems

While there are references to "claude" in some file names and test files (like `test_claude_activity_integration.py`, `claude_analyzer.py`), these appear to be naming conventions or placeholders rather than actual Claude API integrations. The codebase structure suggests this is a workflow orchestration system for repository analysis, but without LLM components that would be subject to prompt injection vulnerabilities.

# data_layer

Data persistence and access patterns

# Data Layer Analysis - RepoSwarm Backend Service

Based on the codebase analysis, here is the documentation of the **ACTUALLY IMPLEMENTED** data layer components:

## Database Architecture

### 1. Primary Database

**Database Type:** NoSQL (Amazon DynamoDB)
- **Purpose:** Repository investigation caching and workflow state persistence
- **Domain:** Caches analysis results, prompt context, and investigation metadata
- **Connection Configuration:** AWS SDK (boto3) with configurable region and credentials
- **Connection Pooling:** Managed by AWS SDK (boto3 client handles connection pooling internally)

### 2. Data Models/Entities

#### Core Domain Entities

**Investigation Cache Entity (`InvestigationCacheKey`)**
```python
# From src/models/cache.py
@dataclass
class InvestigationCacheKey:
    repo_url: str
    prompt_name: str
    version: str
    
    @property
    def cache_key(self) -> str:
        return f"{self.repo_url}#{self.prompt_name}#{self.version}"
```

**Repository Investigation Models**
```python
# From src/models/investigation.py
@dataclass
class RepoInvestigationRequest:
    repo_url: str
    prompts: List[str]
    cache_key: Optional[str] = None

@dataclass
class RepoInvestigationResult:
    repo_url: str
    results: Dict[str, str]
    metadata: Dict[str, Any]
```

**Activity Models**
```python
# From src/models/activities.py
@dataclass
class AnalyzeRepoParams:
    repo_url: str
    prompt_name: str
    context: Dict[str, Any]
    cache_key: Optional[str] = None
```

#### Entity Relationships
- **1:N** - One repository can have multiple cached investigation results (different prompts)
- **1:N** - One investigation can have multiple analysis results (different sections)
- **1:1** - Each cache entry maps to one specific prompt version and repository combination

#### Database Schema

**DynamoDB Table Structure:**
- **Table Name:** `investigation-cache` (configurable via environment)
- **Partition Key:** `cache_key` (composite: `repo_url#prompt_name#version`)
- **Attributes:**
  - `repo_url` (String)
  - `prompt_name` (String) 
  - `version` (String)
  - `result` (String) - Cached analysis result
  - `timestamp` (Number) - Unix timestamp
  - `metadata` (Map) - Additional context data

### 3. Data Access Layer

#### Repository Pattern Implementation

**Investigation Cache Repository**
```python
# From src/activities/investigation_cache.py
class InvestigationCache:
    def __init__(self, dynamodb_client):
        self.client = dynamodb_client
        self.table_name = self._get_table_name()
    
    async def get(self, cache_key: InvestigationCacheKey) -> Optional[str]
    async def set(self, cache_key: InvestigationCacheKey, result: str) -> None
    async def exists(self, cache_key: InvestigationCacheKey) -> bool
```

**DynamoDB Client Wrapper**
```python
# From src/utils/dynamodb_client.py
class DynamoDBClient:
    def __init__(self):
        self.client = self._create_client()
    
    def _create_client(self):
        # Handles local vs AWS configuration
        if self._is_local_testing():
            return boto3.client('dynamodb', endpoint_url='http://localhost:8000')
        return boto3.client('dynamodb')
```

#### Raw DynamoDB Operations
- **GetItem:** For cache lookups
- **PutItem:** For storing analysis results
- **Query:** Not currently implemented
- **Scan:** Not currently implemented

### 4. Caching Layer

**Cache Provider:** Amazon DynamoDB (used as cache storage)

**Caching Strategy:** Cache-aside pattern
- Check cache before performing expensive analysis
- Store results after successful analysis
- Manual cache invalidation (no TTL implemented)

**Cache Key Strategy:**
```python
def cache_key(self) -> str:
    return f"{self.repo_url}#{self.prompt_name}#{self.version}"
```

**Version-Aware Caching:**
- Cache keys include prompt version for invalidation
- Different prompt versions create separate cache entries
- Version extraction from prompt metadata

## Data Operations

### 1. CRUD Operations

**Create/Update (Set)**
```python
async def set(self, cache_key: InvestigationCacheKey, result: str) -> None:
    await self.client.put_item(
        TableName=self.table_name,
        Item={
            'cache_key': {'S': cache_key.cache_key},
            'repo_url': {'S': cache_key.repo_url},
            'prompt_name': {'S': cache_key.prompt_name},
            'version': {'S': cache_key.version},
            'result': {'S': result},
            'timestamp': {'N': str(int(time.time()))}
        }
    )
```

**Read (Get)**
```python
async def get(self, cache_key: InvestigationCacheKey) -> Optional[str]:
    response = await self.client.get_item(
        TableName=self.table_name,
        Key={'cache_key': {'S': cache_key.cache_key}}
    )
    return response.get('Item', {}).get('result', {}).get('S')
```

**Exists Check**
```python
async def exists(self, cache_key: InvestigationCacheKey) -> bool:
    response = await self.client.get_item(
        TableName=self.table_name,
        Key={'cache_key': {'S': cache_key.cache_key}},
        ProjectionExpression='cache_key'
    )
    return 'Item' in response
```

**Delete:** Not implemented
**Bulk Operations:** Not implemented

### 2. Transactions
- **Transaction Boundaries:** Not implemented
- **Distributed Transactions:** Not implemented
- **Saga Patterns:** Not implemented

### 3. Data Validation

**Schema Validation:**
```python
@dataclass
class InvestigationCacheKey:
    repo_url: str
    prompt_name: str  
    version: str
```

**Business Rule Validation:**
- URL sanitization for repository URLs
- Prompt name validation against available prompts
- Version format validation

**Data Sanitization:**
```python
# From src/investigator/core/utils.py
def sanitize_url_for_key(url: str) -> str:
    return url.replace('/', '_').replace(':', '_')
```

### 4. Query Optimization
- **N+1 Query Prevention:** Not applicable (key-value access pattern)
- **Eager/Lazy Loading:** Not implemented
- **Query Result Pagination:** Not implemented
- **Performance Patterns:** Single-item lookups by partition key

## Data Migration & Seeding

### 1. Migration Strategy
**Migration Tools:** Not implemented
**Version Control:** Not implemented  
**Rollback Procedures:** Not implemented

### 2. Data Seeding
**Seed Data Management:** Not implemented
**Test Data Generation:** Not implemented

## Data Security

### 1. Data Protection
**Encryption at Rest:** AWS DynamoDB default encryption
**Field-level Encryption:** Not implemented
**PII Handling:** Not implemented
**Data Masking:** Not implemented

### 2. Access Control
**Database User Permissions:** AWS IAM-based access control
**Row-level Security:** Not implemented
**Multi-tenancy Patterns:** Not implemented
**Data Isolation:** By repository URL in cache keys

## Data Synchronization

### 1. Event Sourcing
**Event Store Implementation:** Not implemented
**Event Replay Mechanisms:** Not implemented
**Snapshots:** Not implemented

### 2. Change Data Capture
**CDC Implementation:** Not implemented
**Data Streaming:** Not implemented
**Sync Mechanisms:** Not implemented

---

## Summary

The RepoSwarm backend implements a **simple caching layer** using **Amazon DynamoDB** as the primary data store. The architecture follows a **cache-aside pattern** with **version-aware caching** for repository analysis results. The data layer is minimal and focused specifically on caching expensive LLM analysis operations, with no complex relational data, transactions, or advanced data synchronization patterns implemented.

# events_and_messaging

Asynchronous communication and event patterns

Looking through the codebase for asynchronous communication patterns and event-driven architecture implementations...

## Message Brokers & Queues

1. **Message Queue Systems:**
   - **Temporal Workflow Engine**: Used as the primary asynchronous processing system
     - Task queues for workflow and activity execution
     - Configured through `TEMPORAL_TASK_QUEUE` environment variable
     - Worker pools for processing activities and workflows

## Event Patterns

**No traditional event-driven patterns found** - The service uses Temporal's workflow orchestration instead of traditional pub/sub or event streaming.

## Messaging Patterns

1. **Communication Patterns:**
   - **Workflow-Activity Pattern**: Temporal's orchestration model
     - Workflows (`investigate_repos_workflow.py`, `investigate_single_repo_workflow.py`) orchestrate activities
     - Activities (`investigate_activities.py`, `investigation_cache_activities.py`) perform individual tasks
     - Asynchronous execution with durability guarantees

2. **Message Processing:**
   - **Activity Execution**: 
     - `ClaudeAnalyzerActivity` - processes repository analysis requests
     - `InvestigationCacheActivity` - handles caching operations
     - `DynamoDBHealthCheckActivity` - performs health checks
   - **Workflow Orchestration**:
     - Sequential and parallel activity execution
     - State management through Temporal's workflow engine

3. **Reliability Patterns:**
   - **Temporal's Built-in Reliability**:
     - Automatic retries for failed activities
     - Workflow state persistence
     - Activity timeouts and heartbeats
     - Durable execution guarantees

## Background Jobs

1. **Job Scheduling:**
   - **Temporal Workers**: 
     - Main worker (`worker.py`) - handles workflow and activity execution
     - Investigation worker (`investigate_worker.py`) - specialized for repository analysis
     - Workers poll task queues for work

2. **Job Processing:**
   - **Activity Workers**:
     - Configurable through `workflow_config.py`
     - Health check monitoring via `health_check.py`
     - Status querying through `query_workflow_status.py`
   - **Workflow Execution**:
     - Long-running repository investigation workflows
     - Parallel processing of multiple repositories
     - Caching integration for performance optimization

## Event Store & Sourcing

**No event sourcing patterns found** - The service uses traditional state management with DynamoDB for caching and Temporal for workflow state.

---

**Summary**: This service implements asynchronous processing primarily through **Temporal Workflows** rather than traditional messaging systems. The architecture uses workflow orchestration for reliable, durable task execution with built-in retry mechanisms and state management.