# agents and things

A collection of tools and utilities used in workflows/proof-of-concepts for research, productivity and business.

## Overview

This repository serves as a workshop for creating, testing, and refining practical AI-powered tools that solve real problems. Think of it as both a laboratory and a parts bin - a place where experimental tools are prototyped, tested in real-world scenarios, and eventually graduated to standalone projects when proven useful.

The collection focuses on agent-based workflows, LLM integration patterns, and automation utilities that can be composed together to build increasingly sophisticated systems. Each component is designed to be self-contained and easily transportable, following the "build once, use anywhere" philosophy.

Rather than rebuilding similar functionality across multiple projects, we develop core patterns here first, refine them through practical use, then copy or adapt the validated implementations to other projects as needed. This approach accelerates development, ensures consistency, and creates a growing library of battle-tested solutions that can be quickly deployed to address new challenges.

### What are Agents and Workflows?

We make an important architectural distinction between two types of systems:

- **Workflows** are systems where LLMs and tools are orchestrated through predefined code paths.
- **Agents** are systems where LLMs dynamically direct their own processes and tool usage, maintaining control over how they accomplish tasks.

Both approaches have their place in building effective AI systems, depending on the requirements of your use case.

## Core Agent Design Principles

When implementing agents, we follow three core principles:

1. **Simplicity**: Maintain simplicity in your agent's design. Start with the simplest solution and only increase complexity when needed.
2. **Transparency**: Prioritize transparency by explicitly showing the agent's planning steps and decision-making process.
3. **Thoughtful Interfaces**: Carefully craft your agent-computer interface through thorough tool documentation and testing. Consider this as important as designing human-computer interfaces.

## Common Agent Patterns

The following patterns represent effective ways to structure agent-based systems:

### Workflow Patterns

1. **Prompt Chaining**: Decompose tasks into sequential steps where each LLM call processes the output of the previous one.
   - *When to use*: Ideal for tasks that can be cleanly decomposed into fixed subtasks.
   - *Examples*: Content generation with editing, translation of specialized content.

2. **Routing**: Classify inputs and direct them to specialized followup tasks.
   - *When to use*: For complex tasks with distinct categories better handled separately.
   - *Examples*: Customer service triage, optimizing model selection based on query complexity.

3. **Parallelization**: Process tasks simultaneously and aggregate results.
   - *When to use*: When subtasks can be parallelized or when multiple perspectives are needed.
   - *Examples*: Implementing guardrails, automated evaluations, code review.

4. **Orchestrator-Workers**: A central LLM dynamically breaks down tasks, delegates to workers, and synthesizes results.
   - *When to use*: For complex tasks where subtasks can't be predetermined.
   - *Examples*: Coding projects spanning multiple files, comprehensive search tasks.

5. **Evaluator-Optimizer**: One LLM generates a response while another evaluates and provides feedback in a loop.
   - *When to use*: When clear evaluation criteria exist and iterative refinement adds value.
   - *Examples*: Literary translation, complex search requiring multiple rounds.

### Autonomous Agents

Fully autonomous agents plan and operate independently, using tools and gaining ground truth from the environment at each step. They handle sophisticated tasks, but their implementation can be straightforward—typically just LLMs using tools based on environmental feedback in a loop.

- *When to use*: For open-ended problems where predicting the required steps is difficult.
- *Examples*: Complex coding tasks, research assistants, autonomous virtual assistants.


## General Guidelines

- **Easy Setup**: Everything should be runnable by setting environment variables and installing `uv`. uv is prefered tool for all use, for single file things use uvx and for modules use pyproject.toml.
  - Create uv Dockerfile for containerized use
  - Include dependencies in uvx script file or pyproject.toml
  - Document any system dependencies beyond Python and other need to know info
- **Documentation**: Every component should include documentation:
  - Single-file tools: Documentation at the beginning of the file
  - Multi-file modules: Dedicated README.md
  - Include usage examples and expected outputs
  - Document environment variables and configuration options
- **Accessibility**: Keep dependencies minimal and provide clear setup instructions
  - Support both local and cloud-based execution models
  - Design for extensibility and composability
  - Follow consistent naming and organization patterns

## Future Ideas

### "Interesting Content Handler"
Process links or messages and extract valuable information:

- **Input Handling**:
  - **Links**: Open, analyze and archive web content
    - **Content Extraction**:
      - HTML parsing with Beautiful Soup or similar
      - JavaScript rendering via Playwright/Puppeteer for dynamic content
      - PDF extraction capabilities for document links
    - **Archiving Strategies**:
      - Local storage with metadata
      - Integration with notion, obsidian or other knowledge bases
      - Version tracking for content that changes over time
    - **Analysis Pipelines**:
      - Topic extraction and categorization
      - Entity recognition for people, companies, concepts
      - Sentiment analysis for opinion pieces
  - **Messages**: Analyze text and extract potential action items
    - **Classification Systems**:
      - Urgency detection (immediate, soon, someday)
      - Task vs information vs request categorization
      - Personal vs work context recognition
    - **Action Extraction**:
      - Deadline identification and calendar integration
      - Responsibility assignment (self vs others)
      - Dependency mapping between tasks
    - **Follow-up Mechanisms**:
      - Reminder generation based on deadlines
      - Status tracking for ongoing actions
      - Completion verification prompts

- **LLM Integration**:
  - Support multiple LLM providers through a flexible configuration system
    - **Provider Adapters**:
      - OpenAI (GPT-3.5, GPT-4)
      - Anthropic (Claude models)
      - Open source models via local endpoints
      - Hybrid approaches for cost/performance optimization
    - **Authentication Management**:
      - Secure API key storage
      - Token usage tracking and limits
      - Rate limiting and retry logic
  - Use generic interfaces like [just-prompt](https://github.com/disler/just-prompt)
    - **Abstraction Layers**:
      - Provider-agnostic prompting API
      - Response normalization
      - Error handling and fallback strategies
  - Configure via .env files with provider-specific settings
    - **Configuration Parameters**:
      - Model selection per task type
      - Cost control thresholds
      - Performance tuning options

### "Agent Collaboration Framework"
Enable multiple specialized agents to work together on complex tasks:

- **Agent Types**:
  - **Research Agents**:
    - **Information Gathering**:
      - Web search integration
      - Database querying capabilities
      - Literature review automation
    - **Synthesis Functions**:
      - Cross-source validation
      - Contradictory information highlighting
      - Knowledge gap identification
  - **Planning Agents**:
    - **Task Decomposition**:
      - Goal breakdown into actionable steps
      - Resource requirement estimation
      - Timeline development
    - **Optimization Strategies**:
      - Critical path identification
      - Parallelization opportunities
      - Risk assessment and mitigation plans
  - **Execution Agents**:
    - **Task Management**:
      - Progress monitoring
      - Blocker identification
      - Adaptive replanning
    - **Output Generation**:
      - Document creation
      - Code generation
      - Visual asset production

- **Collaboration Mechanisms**:
  - **Communication Protocols**:
    - **Standardized Message Formats**:
      - Request/response patterns
      - Broadcast notifications
      - Status update templates
    - **Routing Logic**:
      - Direct agent-to-agent communication
      - Centralized coordinator patterns
      - Publish-subscribe models
  - **Shared Knowledge Base**:
    - **Storage Solutions**:
      - In-memory for ephemeral projects
      - Persistent storage for long-running tasks
      - Versioned history for auditing
    - **Access Patterns**:
      - Read/write permissions per agent
      - Conflict resolution strategies
      - Knowledge retrieval optimization

## LLM Query Framework

Standard components for interacting with LLMs:

- **Prompt Engineering**
  - System-specific instructions and user request
    - **Role Definition**:
      - Expert persona specification
      - Responsibility scope
      - Ethical guidelines and constraints
    - **Task Framing**:
      - Goal clarification
      - Success criteria
      - Output format requirements
  - **Context Management**
    - **Relevance Filtering**:
      - Priority ranking of context elements
      - Recency weighting for time-sensitive information
      - Source credibility assessment
    - **Representation Strategies**:
      - Text chunking and window approaches
      - Hierarchical summarization for large contexts
      - Multi-modal context inclusion (text + images)

- **Context**
  - Relevant background information
    - **Domain Knowledge**:
      - Technical concepts and terminology
      - Historical data and precedents
      - Current state information
    - **User-Specific Information**:
      - Preferences and past interactions
      - Skill level and familiarity
      - Goals and motivations
  - General knowledge/styles/guidelines
    - **Stylistic Parameters**:
      - Formality level
      - Technical depth
      - Tone and voice characteristics
    - **Organizational Standards**:
      - Compliance requirements
      - Branding guidelines
      - Documentation formats

- **Model Configuration**
  - LLM model selection
    - **Selection Criteria**:
      - Task complexity requirements
      - Specialized capabilities needed
      - Cost vs. performance tradeoffs
    - **Versioning Strategy**:
      - Stable vs. experimental models
      - Fallback hierarchies
      - A/B testing frameworks
  - Generation parameters
    - **Temperature Tuning**:
      - Creative vs. deterministic tasks
      - Exploration vs. exploitation balance
      - Adaptive temperature based on confidence
    - **Sampling Controls**:
      - Top-p and top-k filtering
      - Repetition penalties
      - Frequency and presence penalties

- **Tools Integration**
  - Available tools ecosystem
    - **Tool Categories**:
      - Data retrieval (search, database access)
      - Computational (calculators, simulators)
      - External APIs (weather, stocks, etc.)
    - **Tool Selection Logic**:
      - Relevance to current task
      - Cost/latency considerations
      - Success probability estimation
  - Tool orchestration
    - **Execution Patterns**:
      - Sequential vs. parallel tool calls
      - Conditional branching based on results
      - Retry strategies for failed tool calls
    - **Result Integration**:
      - Merging multiple tool outputs
      - Resolving conflicting information
      - Formatting for human readability

## Response Processing

- **Output Analysis**
  - Generated text evaluation
    - **Quality Assessment**:
      - Completeness check
      - Accuracy verification
      - Coherence evaluation
    - **Safety Filtering**:
      - Content policy compliance
      - Bias detection
      - Harmful output prevention
  - Structured data extraction
    - **Parsing Strategies**:
      - JSON/XML schema validation
      - Named entity recognition
      - Key-value extraction
    - **Normalization Processes**:
      - Data type conversion
      - Unit standardization
      - Format harmonization

- **Action Management**
  - Task tracking systems
    - **Status Workflows**:
      - New → In Progress → Completed → Verified
      - Priority adjustments based on context
      - Dependency management
    - **Integration Points**:
      - Task management tools (Jira, Asana, etc.)
      - Calendar systems
      - Notification services
  - Feedback loops
    - **User Feedback Collection**:
      - Explicit ratings and comments
      - Implicit signals (usage patterns)
      - A/B testing of alternative approaches
    - **Model Improvement**:
      - Fine-tuning datasets creation
      - Prompt refinement based on outcomes
      - System adaptation to user preferences

## References & Resources

- [Single File Agents](https://github.com/disler/single-file-agents) - Examples of self-contained agent implementations
- [Just Prompt](https://github.com/disler/just-prompt) - Generic LLM prompting interface

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

- **Getting Started**:
  - Fork the repository
  - Create a feature branch
  - Add your contribution
  - Submit a pull request with detailed description
- **Code Standards**:
  - Follow PEP 8 guidelines
  - Include appropriate tests
  - Document public interfaces

## License

[Your chosen license]
