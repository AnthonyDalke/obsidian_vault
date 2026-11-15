1. Draft a simple consisting of the following sections
	1. Feature name or brief description
	2. Goal
	3. Requirements
	4. Out of scope
2. Translate the requirements into tests, with a prompt like:
	- "Read the [feature name] specification. Create tests for each requirement and important edge case. Include successful and failure cases, along with security-related cases [optional]. Do not implement the feature yet. Keep the tests focused on the behavior described in the spec. List any unclear requirements instead of guessing. After writing the tests, explain what each test covers, and identify any gaps."
	- Make sure to actually review the generated tests
3. Run the tests
4. Have the agent plan the implementation while considering the existing architecture of the codebase
	- Prompt the agent to inspect both the codebase and spec, propose a step-by-step implementation, and explain trade-offs
	- Review the output
5. Proceed with the agent building the feature/spec
	- Supply the spec, tests, implementation plan, and any desired guidance (e.g., project conventions)
	- Instruct the agent to build in small steps, running appropriate tests as it goes, with a warning to not simply weaken failing tests
	- Add instructions to surface contradictory or unclear guidance rather than change the spec
6. Verify the test and code output