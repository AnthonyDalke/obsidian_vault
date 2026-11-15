- Harness Skills to encode "procedural knowledge"
- [agentskills.io] defines standards
- The agent loads only the YAML frontmatter name and description at startup, then the actual definition when triggered
- In descriptions, lean toward over-, rather than under-describing capabilities, since agents tend to under-trigger Skills
- Document findings from needing to correct the agent in the body of the Skills files
	- i.e., If output doesn't meet expectations, account for it
- The body of the files loads into context when triggered, so utilize space judiciously
	- Try to limit to 500 lines, by focusing only on info the LLM would not already have
	- When needs exceed a single file, expand into multiple saved in sub-directories, such as references and assets
- When determinism becomes essential, write scripts files in a scripts/ sub-directory
	- The Skill can simply direct the LLM to read and run the scripts file
	- This prevents the LLM from guessing at logic to run
- Skill "audit checks" (hallmarks of a good Skill):
	1. Triggers when applicable
	2. Reflects or encodes real-world expertise
	3. Spends context wisely
	4. Makes use of deterministic scripts for use cases needing reproducibility
	5. Only gets deployed after getting reviewed/vetted