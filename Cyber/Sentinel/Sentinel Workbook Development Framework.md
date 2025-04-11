# Microsoft Sentinel Workbook Development Comprehensive Framework

## Purpose and Context

This document establishes the complete framework for developing Microsoft Sentinel Workbooks that meet professional standards for performance, usability, and maintainability. As you generate Microsoft Sentinel Workbooks, you must follow these specifications exactly to ensure the output meets security operations requirements. This document serves as your authoritative reference for all Sentinel Workbook development decisions.

## Core Components

A Microsoft Sentinel Workbook consists of these specific components that you must implement correctly:

1. **Parameters**: User input controls that filter or modify visualizations
2. **Queries**: KQL code that retrieves and processes log data
3. **Visualizations**: Charts, tables, and graphics that display query results
4. **Text elements**: Instructions, context, and explanations for users
5. **Tabs**: Organizational dividers that separate workbook sections
6. **Links**: Connections to other workbooks or external resources

You must ensure all components work together cohesively while following the exact standards defined in this document.

## Design Framework

### Workbook Structure Specification

When generating a workbook, you must implement this exact structural hierarchy:

1. **First level: Tabs**
   - Each tab must focus on a distinct analytical purpose
   - Tab names must be concise nouns (Overview, Investigation, Configuration)
   - Tabs must progress from general to specific information

2. **Second level: Sections within tabs**
   - Each section must group related visualizations with a clear heading
   - Sections must be visually separated with consistent spacing (20px minimum)
   - Sections must include explanatory text above visualizations

3. **Third level: Parameter groups**
   - Parameters must appear at the top of tabs in logical groups
   - Related parameters must be placed horizontally adjacent
   - Dependent parameters must use cascading arrangements

4. **Fourth level: Visualization arrangements**
   - Related visualizations must be aligned in grid layouts
   - Information hierarchy must flow top-to-bottom and left-to-right
   - Visualization size must reflect information importance

### Naming Convention Rules

You must apply these exact naming patterns:

1. **Workbook names**: `[DataSource]-[AnalysisFocus]-Workbook`
   - Example: `AzureActivity-AdminOperations-Workbook`
   - Example: `SecurityEvent-AuthenticationAnalysis-Workbook`

2. **Parameter names**: `param[CategoryName][Function]`
   - Example: `paramTimeRange`
   - Example: `paramResourceGroup`
   - Example: `paramAlertSeverity`

3. **Query variable names**: `[dataType][Operation][Filter]`
   - Example: `securityAlertsFiltered`
   - Example: `authenticationFailuresByAccount`
   - Example: `networkConnectionsExternal`

4. **Tab names**: `[Domain][AnalysisType]`
   - Example: `OverviewSummary`
   - Example: `AlertsDetailed`
   - Example: `UserInvestigation`

You must never deviate from these naming conventions as they ensure consistent interpretation by both humans and automated systems.

## Query Development Requirements

### KQL Structure Standards

Every KQL query you generate must follow this exact structure:

```kql
// PURPOSE: [Clear description of query purpose]
// PARAMETERS: [List of parameters used]
// TABLES: [Data sources/tables accessed]
// RETURNS: [Description of result schema]
// Define parameters and variables
let timeRange = {TimeRange:value};
let threshold = {ThresholdValue:value};
// Main data acquisition
let baseData = 
    [TableName]
    | where TimeGenerated >= ago(timeRange)
    | where [column] == "[value]"
    | project [columns to keep];
// Data transformation and analysis
let analysisResults = 
    baseData
    | summarize [aggregations] by [dimensions]
    | where [filtering conditions];
// Final output preparation
analysisResults
| order by [sortColumn] desc
| project [final columns in display order]
```

This structure is mandatory for all queries to ensure readability, performance, and maintainability.

### KQL Formatting Requirements

You must follow these exact KQL formatting rules:

1. **No blank lines**
   - Never include blank lines in KQL queries
   - Blank lines can cause parsing errors in Sentinel workbooks
   - Use comments and indentation for readability instead of blank lines

2. **Comment formatting**
   - Prefix all comments with `//` followed by a single space
   - Use comments before logical sections of the query
   - Comments should be concise and descriptive

3. **Indentation standards**
   - Indent pipe operations with 4 spaces
   - Align related operations at the same indentation level
   - Maintain consistent indentation throughout the query

4. **Line continuation**
   - Each pipe operator (`|`) must start a new line
   - Continue long expressions on the same line when possible
   - For lengthy expressions, align continuations with proper indentation

Example of correctly formatted KQL without blank lines:

```kql
// Query to identify high-volume login failures
let timeFrame = {TimeRange:value};
let failureThreshold = {FailureThreshold:value};
// Filter to relevant security events
SecurityEvent
| where TimeGenerated >= ago(timeFrame)
| where EventID == 4625
| where AccountType == "User"
// Aggregate and analyze failures
| summarize 
    FailureCount = count(), 
    LastFailure = max(TimeGenerated) 
    by Account, Computer
| where FailureCount >= failureThreshold
| order by FailureCount desc
| project Account, Computer, FailureCount, LastFailure
```

### Parameter Implementation Requirements

You must implement these exact parameter types and configurations:

1. **Time Range Parameter**
   ```kql
   // Required time range parameter implementation
   let _TimeRange = {TimeRange:value};
   let _StartTime = ago(_TimeRange);
   let _EndTime = now();
   ```

2. **Resource Filter Parameter**
   ```kql
   // Required resource filter parameter implementation
   let _SelectedSubscriptions = 
       dynamic([{Subscription:value}]);
   let _SelectedResourceGroups = 
       dynamic([{ResourceGroup:value}]);
   ```

3. **Threshold Parameter**
   ```kql
   // Required threshold parameter implementation
   let _AlertThreshold = {AlertThreshold:value};
   let _WarningThreshold = {WarningThreshold:value};
   ```

4. **Dropdown Selection Parameter**
   ```kql
   // Required dropdown parameter implementation
   let _SelectedSeverity = 
       dynamic([{Severity:label}]);
   let hasSeverityFilter = 
       array_length(_SelectedSeverity) > 0;
   ```

### Error Handling Requirements

You must implement this exact error handling pattern in all queries:

```kql
// 1. Check for data existence
let hasData = toscalar([Table] | where TimeGenerated >= ago(_TimeRange) | take 1 | count > 0);
// 2. Create empty dataset with correct schema
let emptyDataset = datatable(
    [Column1]:[Type1], 
    [Column2]:[Type2],
    [Column3]:[Type3]
)[];
// 3. Run actual query with fallback to empty dataset
let results = iff(hasData,
    [Table]
    | where TimeGenerated >= ago(_TimeRange)
    | where [filtering conditions]
    | summarize [aggregations] by [dimensions],
    emptyDataset
);
// 4. Add error messaging
results
| extend ErrorMessage = iff(hasData, "", "No data available for the selected time period")
```

This pattern is mandatory for all queries to handle empty result sets gracefully.

### Query Performance Requirements

You must optimize every query according to these exact specifications:

1. **Filtering optimization**
   - Apply time filters first using `TimeGenerated >= ago(_TimeRange)`
   - Apply high-cardinality filters early (subscription, resource group)
   - Use in operator for multi-value filters: `| where EventID in (4624, 4625)`

2. **Column selection optimization**
   - Project only necessary columns immediately after filtering
   - Use extend only for computed columns, not for renaming
   - Limit string manipulations to only required columns

3. **Aggregation optimization**
   - Pre-filter data before performing summarize operations
   - Use max bin count of 50 for time chart visualizations
   - Limit make_list and make_set to 100 items maximum

4. **Join optimization**
   - Filter both sides of joins before joining
   - Use inner join by default, left outer only when necessary
   - Include explicit time constraints on both sides of joins

## Visualization Selection Requirements

You must select visualizations based on these exact data type mappings:

1. **Time series data**
   - Primary: Line chart
   - Secondary: Area chart
   - Requirements: datetime dimension with max 100 points

2. **Categorical comparisons**
   - Primary: Bar chart (horizontal for >7 categories)
   - Secondary: Column chart (vertical for ≤7 categories)
   - Requirements: string dimension with count/sum/avg measure

3. **Tabular data**
   - Primary: Grid view
   - Secondary: List view
   - Requirements: >3 columns use grid, ≤3 columns use list

4. **Status indicators**
   - Primary: Stat visualization
   - Secondary: Status tiles
   - Requirements: Single numeric value with optional trend

5. **Geographical data**
   - Primary: Map visualization
   - Requirements: Include latitude/longitude or country/region fields

6. **Entity relationships**
   - Primary: Graph visualization
   - Requirements: Source and target entities with relationship type

## Accessibility Requirements

You must implement these exact accessibility specifications:

1. **Color schemes**
   - Primary blue: #0078D4
   - Alert red: #D13438
   - Warning orange: #FF8C00
   - Success green: #107C10
   - Neutral gray: #605E5C

2. **Text requirements**
   - Heading size: 16px minimum
   - Body text size: 14px minimum
   - Label size: 12px minimum
   - Contrast ratio: 4.5:1 minimum

3. **Interactive element sizing**
   - Buttons: 32px height minimum
   - Checkboxes: 20px square minimum
   - Dropdown controls: 32px height minimum

## Performance Optimization Requirements

You must implement these exact performance optimizations:

1. **Query limitations**
   - Maximum time range: 30 days for raw event queries
   - Maximum result set: 50,000 rows before aggregation
   - Maximum join complexity: 3 joins per query maximum
   - Maximum run time: 60 seconds maximum

2. **Visualization limitations**
   - Maximum visualizations per tab: 8
   - Maximum data points per chart: 1,000
   - Maximum table rows displayed: 100 (use pagination)
   - Maximum refresh frequency: 5 minutes

3. **Resource efficiency**
   - Materialize reused datasets using the let keyword
   - Share query results across multiple visualizations
   - Implement progressive loading for complex visualizations

## RBAC Implementation Requirements

You must implement these exact RBAC configurations:

1. **Role specifications**
   ```
   Viewer Role: Microsoft Sentinel Reader
   Analyst Role: Microsoft Sentinel Responder
   Administrator Role: Microsoft Sentinel Contributor
   ```

2. **Documentation requirements**
   - List required roles in workbook header text
   - Specify permission requirements for each tab
   - Document any custom role requirements

## Implementation Example Templates

### Security Monitoring Workbook Template

```
Tab 1: Overview
- Time Range Parameter (default: 24h)
- Subscription Filter Parameter
- Alert Summary Visualization (Stat)
- Alert Trend Visualization (Line Chart)
- Top Resources Visualization (Bar Chart)
- Top Users Visualization (Bar Chart)

Tab 2: Alert Investigation
- Entity Selection Parameter
- Alert Timeline Visualization (Time Chart)
- Alert Detail Visualization (Grid)
- Related Entities Visualization (Graph)

Tab 3: User Activity
- User Selection Parameter
- Authentication Visualization (Line Chart)
- Operation Visualization (Grid)
- Resource Access Visualization (Grid)

Tab 4: Documentation
- Purpose Description Text
- Data Sources List
- Update History
- Contact Information
```

### Threat Hunting Workbook Template

```
Tab 1: Hunt Overview
- Time Range Parameter (default: 7d)
- Resource Filter Parameter
- Hunting Lead Summary Visualization (Tiles)
- Anomaly Detection Visualization (Time Chart)
- Behavioral Outliers Visualization (Scatter Plot)

Tab 2: IOC Matching
- IOC Type Parameter
- IOC Value Parameter
- Match Results Visualization (Grid)
- Historical Context Visualization (Time Chart)

Tab 3: MITRE ATT&CK
- Technique Selection Parameter
- Tactic Coverage Visualization (Heat Map)
- Detection Coverage Visualization (Grid)
- Evidence Collection Visualization (Grid)

Tab 4: Documentation
- Hunting Methodology Text
- Query Explanations
- False Positive Guidance
- Escalation Procedures
```

## Anti-Pattern Prohibitions

You must never implement these anti-patterns in your workbook development:

1. **Query anti-patterns**
   - Using `*` in project statements
   - Performing string operations before filtering
   - Using nested summarize operations
   - Joining tables without size reduction first
   - Hardcoding time ranges or resource names
   - Including blank lines in KQL queries
   - Using tabs or spaces in otherwise blank lines
   - Inconsistent indentation between pipe operations

2. **Visualization anti-patterns**
   - Using pie charts with >7 segments
   - Creating dashboards with >10 visualizations per tab
   - Implementing visualizations without clear titles
   - Using red/green color schemes (inaccessible)
   - Displaying raw data without aggregation

3. **Parameter anti-patterns**
   - Creating parameters without default values
   - Implementing circular parameter dependencies
   - Using unclear parameter labels
   - Creating unnecessary parameters
   - Failing to validate parameter inputs

4. **Structure anti-patterns**
   - Creating single-tab workbooks with excessive scrolling
   - Implementing inconsistent navigation patterns
   - Using inconsistent naming conventions
   - Creating monolithic workbooks rather than linked ones
   - Failing to provide documentation tabs

## Implementation Process Requirements

When implementing a workbook, you must follow this exact process:

1. **Planning phase**
   - Define clear objectives and user stories
   - Identify all required data sources
   - Map out tab structure and navigation flow
   - Define parameter requirements
   - Plan visualization layout

2. **Development phase**
   - Create parameters first
   - Develop and test queries individually
   - Implement visualizations with sample data
   - Connect queries to visualizations
   - Add instructional text and documentation

3. **Testing phase**
   - Validate parameters function correctly
   - Verify queries execute within time limits
   - Confirm visualizations render properly
   - Test with different screen sizes
   - Verify error handling works correctly

4. **Documentation phase**
   - Document workbook purpose and usage
   - List all parameters with descriptions
   - Explain data sources and refresh rates
   - Provide interpretation guidance
   - Include contact information for support

## Final Output Requirements

Your final workbook output must include:

1. **JSON Template**: The complete ARM template for the workbook
2. **Query Library**: All KQL queries extracted for reference
3. **Parameter Documentation**: All parameters with descriptions
4. **Visual Layout Documentation**: Tab and visualization structure
5. **User Guide**: Instructions for using the workbook

You must validate your output against all requirements in this document before delivering it to ensure complete compliance with Microsoft Sentinel Workbook development standards.
