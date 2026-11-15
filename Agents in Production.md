1. Lifecycle management: proper change reviews and access granting only as necessary
2. Security and IAM: assigning identities to agents and enforcing appropriate privileges and guardrails according to tasks at hand
	- Identities/roles become necessary not just to ensure only the desired changes occur but to safeguard traceability for audit purposes
	- Authentication patterns can get applied multiple ways
		1. Automatically or system-generated - triggered by specific actions rather than specific agents
		2. On-behalf-of-user - connected to privileges of specific users
		3. Manually or with preexisting identities - created by a human ahead of time for specific purposes (e.g., controlling what to run in production)
	- Best practice for MCP: store credentials on the MCP server and authenticate with the agent
3. Risk management: best practices to minimize unintended consequences:
	1. Treat external content as un-trusted - utilize it for reasoning, not instructions for the agent
	2. Separate instructions from data in prompts, to help avoid prompt injection
	3. Add human review to potentially destructive actions
	4. Log agent reasoning
	5. Set and enforce cost guardrails