- General structure to follow
	- General rules: top-level AGENTS.md / CLAUDE.md, to enforce across the board
	- Specific rules: folder/directory-specific AGENTS.md / CLAUDE.md
	- Skills: specific to particular tasks
	- Sub-agents: agents dedicated to particular tasks
	- MCP servers: connections to sources like Jira, Confluence, and data warehouses
- dbt's suggestion for data pipeline guardrails
	- Testing and validation infrastructure: tests/contracts/CI
	- Semantic layer: centralized business logic and definitions
	- Supporting metadata: data or model lineage, ownership, and documentation
	- Local validation compute: resources to quickly run testing and validation infrastructure, without relying on cloud
- Agent-friendly project workflow
	1. Research: expose the agent to the relevant codebase and context, then have it interview (or grill, a la Matt Pocock) the creator with a structured approach
	2. Plan: synthesize the research with other key components listed below into a single spec. document
		1. User story
		2. Problem statement
		3. Task list
		4. Validation strategy
	3. Implement: initiate new agent session to build the spec.
	4. Validate: partner with an agent to run test infrastructure (agent), then review results and changes (human)