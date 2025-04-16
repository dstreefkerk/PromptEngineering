# API Reference Guide: Core Components and Usage

Please examine the current Python codebase and generate concise documentation outlining:

1. All available classes with brief descriptions
2. Public method signatures for each class
3. Important parameter descriptions
4. Return types
5. Key dependencies between components

Format the output as markdown with these specific guidelines:

- Begin with a table of contents (TOC) that links to all major sections
- Use consistent header levels: # for title, ## for major sections, ### for classes, #### for examples and subsections
- Format all lists consistently using "-" bullets (not "*")
- Use tables (| Column1 | Column2 |) for displaying enums, constants, and property sets
- Group long lists alphabetically or by functional category
- Label all code examples with #### headers (e.g., "#### Example: List All Incidents")
- Use consistent double quotes (") in all code examples, not single quotes
- Apply consistent title case capitalisation for all headings
- For large sections with many items, create logical groupings
- Use code blocks with language hints (```python) for all code samples
- Order items within the same heading level alphabetically (classes, methods, properties, etc.)

Keep descriptions brief but informative. Focus on the public API rather than implementation details.

Include examples of common usage patterns if they can be inferred from the code. Organize the documentation hierarchically based on the package structure.

No need to document private methods (prefixed with underscore) unless they're critical for understanding the codebase.

Save this documentation as a markdown file named "API-Reference-Guide-Core-Components-and-Usage.md" in the project's root folder.
