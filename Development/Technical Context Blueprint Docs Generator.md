# AI-Assisted Software Development Documentation Generator

You are an expert in AI-assisted software development and documentation, with deep knowledge of creating structured coding documents for AI coding tools. I need you to generate a complete set of coding documents to provide a robust "context boundary" for an AI model to build my project without hallucinations or errors.

Based on your expertise and best practices, generate the following interconnected documents, ensuring each is detailed, clear, and tailored to the project with specific values rather than general descriptions. Use a narrative style for the System Flow Document (no bullet points), and ensure all documents align with popular tech stacks that AI models are trained on. Maintain consistency across all documents to create a coherent context boundary.

## Project Requirement Document (PRD)
This document serves as the blueprint for the AI model, ensuring it doesn't make assumptions and has all necessary project details.

The PRD must include these specific sections:
1. **Project Overview**: A comprehensive summary of the project's purpose, goals, and vision (be specific about what the system will accomplish)
2. **Target Users/Systems**: Detailed description of primary and secondary users or systems that will interact with the project
3. **Interaction Flow**: High-level description of system interactions and user journeys
4. **Technology Stack Overview**: Brief summary of key technologies (detailed in Tech Stack Document)
5. **Core Features/Capabilities**: Exhaustive list of all functionalities with detailed descriptions of each
6. **Scope Limitations**: Explicit boundaries defining what is excluded from the initial version and what will be addressed in future iterations
7. **Success Criteria**: Specific, measurable outcomes that define project success
8. **Dependencies**: Any external systems, services, or resources the project relies on

## System Flow Document
This narrative document helps the AI create a mental model of the entire system structure and operation.

The System Flow Document must include these aspects in narrative form:
1. **System Initialization**: How the system starts up and initializes its components
2. **Main Operation Flows**: Detailed end-to-end narratives of primary system operations
3. **Component Interactions**: How different parts of the system communicate and share data
4. **Data Transformations**: How information changes as it moves through the system
5. **Error Handling Flows**: How the system responds to various failure scenarios
6. **Edge Cases**: Descriptions of unusual but important system behaviors
7. **Integration Points**: How the system connects with external services or systems
8. **System Boundaries**: Where the system's responsibilities begin and end

Write this document in a conversational, narrative style without bullet points or numbered lists to help the AI construct a mental graph of the system's structure and flow.

## Tech Stack Document
This document specifies the technical foundation of the project to ensure compatibility with AI's training data.

The Tech Stack Document must include these sections:
1. **Programming Languages**: Primary and supporting languages with version requirements
2. **Frontend Technologies** (if applicable): Frameworks, libraries, state management, and UI tools
3. **Backend Technologies**: Server frameworks, APIs, middleware, and runtime environments
4. **Database Technologies**: Database types, query languages, and data storage approaches
5. **Authentication/Authorization**: Identity management and access control systems
6. **Infrastructure**: Hosting, containerization, and deployment platforms
7. **Third-Party Services**: External APIs and services to be integrated
8. **Development Tools**: Build systems, testing frameworks, and developer utilities
9. **Rationale for Choices**: Specific reasons for selecting each technology
10. **Compatibility Notes**: How these technologies work together as a cohesive system

Use widely-adopted, popular frameworks and tools that AI models are likely to be familiar with, providing specific versions for all technologies.

## Frontend Guidelines (if applicable)
This document ensures consistent interface design and implementation.

The Frontend Guidelines must include these sections:
1. **Architecture Pattern**: Component structure, state management approach, and code organization
2. **Design System**: Comprehensive visual language for the project
   - **Color Palette**: Exact color codes (e.g., primary: #1E90FF, not "blue")
   - **Typography**: Font families, weights, sizes, and line heights with specific measurements
   - **Spacing System**: Specific spacing units and when to apply them
   - **Component Library**: Reusable UI elements and their variants
3. **Interaction Patterns**: Standard behaviors for user interactions
4. **Responsive Design Approach**: Specific breakpoints and adaptation strategies
5. **Accessibility Standards**: Compliance requirements and implementation guidelines
6. **Performance Targets**: Loading times, bundle sizes, and optimization techniques
7. **State Management**: How application state should be handled
8. **Error Handling**: How errors should be displayed to users
9. **For APIs/Non-visual Interfaces**: Interface design patterns and response formats

Include exact specifications rather than general guidelines to minimize AI guesswork.

## Backend Structure
This document defines the system's data and service architecture.

The Backend Structure must include these sections:
1. **Data Models**: Complete schemas with all fields, types, constraints, and relationships
   - Field names, data types, validation rules, default values
   - Primary keys, foreign keys, and indexes
   - Entity relationships with cardinality (one-to-many, many-to-many, etc.)
2. **API Contracts**: Detailed endpoint specifications
   - URL patterns, HTTP methods, request parameters
   - Response formats, status codes, and error responses
   - Authentication requirements for each endpoint
3. **Service Architecture**: Breakdown of services/modules and their responsibilities
4. **Storage Strategy**: How and where different types of data are stored
5. **Access Control Policies**: Detailed rules for who can access what data and when
6. **Integration Patterns**: How the backend connects with external systems
7. **Caching Strategy**: What should be cached and how
8. **Scaling Considerations**: How the system will handle increased load
9. **Transaction Management**: How data consistency will be maintained

Be exhaustive in data model definitions to guide AI in creating correct database schemas.

## Implementation Plan
This step-by-step guide prevents errors like hallucinations, duplicate files, or code deletion.

The Implementation Plan must include:
1. **50 Sequenced Steps**: Numbered steps that build on each other logically, including:
   - Environment setup and configuration
   - Project structure creation
   - Dependency installation
   - Core functionality implementation
   - Integration of components
   - Testing procedures
   - Deployment preparation
2. **File Structure Specifications**: Exact file paths and naming conventions
3. **Error Prevention Guidelines**:
   - Instructions to check for existing files before creation
   - Validation steps before modifying critical components
   - Backup procedures for important data
   - How to handle merge conflicts or overwrites
4. **Checkpoints**: Verification steps to ensure progress is on track
5. **Testing Instructions**: What to test at each stage
6. **Dependency Management**: How to handle package installations and updates
7. **Version Control Practices**: Branching, committing, and merging guidelines

Each step should be specific enough that an AI can follow it without making assumptions.

## Security Guideline Document
This document ensures the system is secure by design from the beginning.

The Security Guideline Document must include these sections:
1. **Core Security Principles**: Fundamental security concepts for the project
2. **Authentication Security**:
   - Authentication mechanisms with specific implementation details
   - Password policies and storage practices
   - Session management specifications
3. **Authorization Framework**:
   - Role-based or attribute-based access control specifications
   - Permission levels and their application
4. **Data Protection**:
   - Encryption standards for data at rest and in transit
   - Data retention and deletion policies
   - Privacy compliance requirements
5. **Input Validation**: Detailed validation rules for all user inputs
6. **Vulnerability Mitigation**:
   - Prevention strategies for common attack vectors (injection, XSS, etc.)
   - Secure coding practices specific to the technology stack
7. **Security Testing**: Required security tests and their frequency
8. **Monitoring and Incident Response**:
   - Security logging requirements
   - Alert thresholds and response procedures
9. **Dependency Security**: Managing and updating dependencies

Provide detailed specifications rather than general advice to enable direct implementation.

Ensure each document is comprehensive, avoids ambiguity, and provides deep context for the AI model to build the project accurately. The entire set should form a cohesive context boundary that guides the AI without allowing for hallucinations or incorrect assumptions. Use specific values, measurements, and specifications throughout to minimize guesswork.