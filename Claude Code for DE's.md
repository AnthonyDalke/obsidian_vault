- Key AI concepts for DE's:

| Concept | Purposes                         | Advantages                                 | Examples                                                 |
| ------- | -------------------------------- | ------------------------------------------ | -------------------------------------------------------- |
| MCP     | Connect to actual data           | Minimize context-switching during sessions | DB's, metadata catalogs                                  |
| Skill   | Enforce best practices           | "Write once, use broadly"                  | Documentation standards, testing practices               |
| Hook    | Automatically run quality checks | "Set it and forget it"                     | Pytest upon commit, SQL linter, dbt test on model change |
- AI-powered data modeling workflow involves Miro, dbt, and Claude
	- Miro MCP captures business context, even meeting notes
	- MCP Data Toolbox compares that business context to contents of a DB
		- Schema YAMLs elucidate data available
	- Claude Skill files take this one step further, such as designing a dbt implementation plan based on the previous step
	- dbt Agent Skills formally generate data models, even with descriptions, "grain docs", and tests
	- The Claude Skill can even generate an ERD for user review
- Workflow to add metadata making existing data consumable by LLMs (all encapsulated in Skill)
	- Measure existing metadata against standards defined in Skill
	- Scan data itself with Postgres MCP to pinpoint edge cases not in metadata
	- Generate missing metadata, or at least highlight it for the user