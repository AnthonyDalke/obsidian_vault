# Agent Fundamentals

- With workflows, the human directs the steps
	- In contrast, agents exercise authority to direct the flow of work
	- In workflows, LLM's function more as "cogs in wheels", rather than the forces _driving_ the wheels
- Agentic loop: Think/Reason -> Act -> Observe -> Repeat
	- Agents call Tools to perform specific actions for the Act component
- Agent architecture patterns
	- Prompt chaining: sequential prompt -> response -> prompt loop
	- Routing: agent routes prompt to tasks for dedicated workflows
	- Parallelization: agent makes multiple Tool calls in parallel
	- Orchestrator-worker: orchestrator agent spawns and coordinates multiple worker agents to perform specific tasks, then synthesizes their output
	- Evaluator-optimizer: evaluation agents produce responses to prompts, which optimizer agents then assess, returning the "feedback" to the evaluator agent for refinement
- System prompts drive agent reasoning and planning
- Agents read from Tool descriptions when identifying Tools to call
- Stopping conditions define when to stop reasoning loops

# Agent Instructions & Context

- Context engineering resembles an ongoing effort of curation, since context affects "a sequence of calls"
- Context engineering best practices
	- Limit system prompts to only the most important behaviors, consigning edge cases to tools or follow up instructions
	- Describe desired behavior with specific, concrete wording
	- Limit tool usage to only those required for a task
	- Ensure clarity in tool descriptions
	- Consolidate similar tools into a single, flexible tool
- System prompt best practices
	- Clearly define roles
	- Place guardrails and limits around tasks
	- Prioritize brevity over completeness
	- Provide examples rather than simply describing desired behavior
	- Explicitly direct to available tools
	- Limit to 200-400 tokens
- `AGENTS.md` / `copilot-instructions.md` files can exist both with a project or workspace or in a user's home directory, to apply more broadly
	- This promotes a version a progressive disclosure, by lower levels overriding higher levels
- Best practices for context management
	- Assess the validity of earlier context after 5-10 exchanges and compact or remove when low
	- Use the `/compact` command to summarize earlier context

# Agent Memory

- Context = information leveraged by LLM specifically at inference
	- In contrast, memory can come in both shorter- and longer-term variants
- Mental model from a computer
	- LLM = CPU
	- Context = RAM
	- Memory = hard drive
- Working memory exists within context
	- Context refers to the location, while working memory refers to the specific information actively retained
- Other types of memory
	- Semantic: guardrails like user preferences and project guidelines
	- Episodic: information from past interactions
	- Persistent: history specifically stored outside context window
- Memory management revolves around five operations
	1. Observe - take in new user actions and information
	2. Select - separate the wheat from the chaff - what to save versus discard
	3. Store - save the information to the appropriate memory store
	4. Retrieve - fetch relevant information into context
	5. Update/forget - prune stored information as appropriate
- Even large context windows demand management
	- Frivolous info makes calls more expensive (more tokens), slower (same reason), and less accurate (contradictory info)
- Information need not get stored; use for working memory, then discard
- Within VS Code, memory exists at three levels: user, session, and repo
	- User (/memories/) - first 200 lines loaded for all of a user's sessions and projects
	- Repo (/memories/repo) - all sessions for a workspace/project
	- Session (/session/session) - specific to individual sessions

# Agent Skills

- Key distinction: system prompts load for every session and call, while Skills only load when called or needed
	- System prompt, along with AGENTS.md = instruction
- Load distinction
	- Instructions: always (principles)
	- Skills: when needed (repeatable workflows)
	- Tools: also when needed (atomic operations)
- In addition to Tools, Skills can encode domain knowledge, instructions or procedures, and supporting resources
- Consider defining a Skill for:
	- Tasks performed more than once or in more than one project
	- Requirements or guidelines stretching beyond what a single prompt could capture (i.e., "Would another team or use case benefit from this guidance?")
	- Tasks benefiting from supporting references
	- Version control to document the actions
	- Tasks only applicable to certain use cases
- In contrast, avoid a Skill for:
	- Concise instructions to apply across-the-board (AGENTS.md or system prompt)
	- Atomic actions (Tool)
- Skills can reside either within a workspace/project or a user's directory
- Rule of thumb: aid discoverability by writing Skill descriptions echoing how you talk about a task

# Tools & MCP

- Tool definitions involve a balance between defining enough to accomplish tasks consistently and repeatedly, without causing LLM's to fixate on deciding *what* to use rather than actually taking actions
- Tool contracts guide interactions between agents and the tools
	- The actual interchange can occur via MCP
- An MCP host (agent) communicates with an MCP server through a Transport
	- This can happen either locally (STDIO) or remotely (HTTP)
		- Local STDIO servers offer more limited functionality but with less latency
		- Remote HTTP servers boast the opposite: greater flexibility but with added latency
- Manage tool exposure with dynamic tool loading or VS Code's Configure Tools feature
# Knowledge & RAG

- RAG begins from the notion of asking an LLM about info outside of its training data
	- "Grounding" = re-orienting
- RAG facilitates grounding with specific documents
- RAG involves documents, which get broken down into chunks, which get broken down into embeddings
	- Documents -> chunks -> embeddings
- Chunks and embeddings get indexed
	- Embeddings also get stored as vectors
- In addition to *what* to retrieve, agents decide *when* and *how* to retrieve knowledge
- Embeddings require context for full effectiveness
- When a user submits a query, the content gets embedded, as well, which enables similarity search for similar vectors, such as with cosine similarity
- Multiple information retrieval methods exist, with different strengths

| Method   | Search Focus                                 | Strength                     |
| -------- | -------------------------------------------- | ---------------------------- |
| Keyword  | Chunks for exact or fuzzy matches            | Precise searches             |
| Semantic | Embeddings within chunks for similar meaning | Intent rather than precision |
| Vector   | Entity-level semantic search                 | More specific intent         |
| Hybrid   | Combination of keyword and semantic          | Flexibility                  |
- RAG only becomes necessary when a knowledge base grows to over 200K tokens, or about 500 pages of text
	- Below that threshold, the added complexity of chunking, retrieving, embedding, etc., can cause more harm than good
	- However, beyond that, RAG's ability to restrict context to only relevant knowledge helps
- RAG can get interpreted automatically, such as in a workflow, or by an agent, when it decides whether it needs the additional knowledge from RAG and how to search it

# Agent Orchestration

- Systems with multiple agents employ separate context windows for each agent
- Sub-agents refer to agents spun up by an orchestrator agent to achieve a specific task
- On the other hand, custom agents have pre-defined personas, tools, or instructions, with the definition occurring in AGENTS.md
- Multi-agent systems consume 3-10x as many tokens and impose considerable operational complexity
- When to expand to multiple agents
	- **Parallelizable tasks**, when a broader task can get broken down into smaller tasks lacking dependencies; e.g., architecture for investigating potential data sources:
		- One agent to examine available schemas, tables, columns, and data types
		- Another to scour terms of service
		- Another to investigate security risks
	- Tasks benefitting from **specialization** from dedicated tools; e.g., from above:
		- Tool with queries like `DESCRIBE`
		- Tool for legal terminology
		- Tool for cyber-security functions
	- Tasks where separation can prevent **context pollution** from the potentially competing demands of the tasks
- When sub-agents "report" back to the orchestrator, they present a summarized version to conserve tokens
- Specialized agents with personas benefit from narrower privileges
	- Least privilege
- In addition to personas, custom agents can come with defined hand-off points