## Skills
- What Skills can capture: "procedural knowledge, steps, conventions, decision points, and best practices"
	- Analogized as an "onboarding guide for a new team member"
- Only introduced as a concept by Anthropic in Oct. 2025
- Considering a tool `validate_table()`, a Skill can distinguish:
	- Which tables to validate first
	- Which validation checks to run
	- How to handle data from diffeMITMITrent domains differently
	- How to ID failures
	- Who to notify of failures
- Structure of Skills.md files
	- YAML "frontmatter", with name and description, surrounded by three hyphens
	- Body, in actual .md syntax
	- Agents examine frontmatter first, so approach it as if for "a teammate with one second to decide on relevance"
	- e.g., "Use when asked to validate, QA, or quality-check a table, or before publishing data to production."
- Progressive Disclosure proceeds in stages
	1. Keep the name and description of all Skills loaded into the System Prompt
	2. Load a body of a Skill only when the name and description indicate its applicability
		- <5K tokens each
	3. Load supporting files, such as Python modules, only as necessary, such as when a Skill calls for them
		- Only load the outputs, not the code itself

## Sub-Agents
- Similar conceptually to distributed processing, where smaller "workers" get orchestrated by a "master"
	- The difference comes in the form of the autonomy of the workers
- When to use
	- Data grows too large for one context window
	- Independent tasks need faster execution through parallelism
- Mechanically, implementation consists of defining an agent with its own system prompt and task
	- Either through an API (programatically) or Claude Code (.md file with YAML formatter in `~/.claude/agents/`)
- The orchestrator can simply take the form of a Python script that calls the sub-agents with their dedicated system prompts and tasks
- Tasks requiring clarification or discussion can cause the sub-agent pattern to break down, presumably by limiting the sub-agents' autonomy

## Memory
- By default, LLM's have a stateless nature
- Two types of memory exist: short- and long-term
	- Short-term: within a given session
	- Long-term: extending across sessions
		- Requires concerted management
		- Also known as episodic memory
- At a fundamental level, memory management involves reading from a file or data source that lays out history - results of prior runs, incorporates that into the current run, then updates a file or data source with new results
	- Analogous to ETL
- However, the specifics of what memory should capture differ
	- Aggregations keep storage lean
	- Watch out for PII
- Storage types for memory, each with strengths
	- Files (e.g., JSON): simple
	- Relational DB's: efficient storage
	- Key-value stores: fast lookups and comment access
	- Vector DB's: semantic context and unstructured
- Best practices
	- Key metrics like row count, freshness, and prior anomaly examples often provide enough benefit
	- Truncate history after certain points or aggregate it to weekly (or more) summaries
	- Attach versions to enable the LLM's to understand history
	- Manually review new memory stores for PII and governance