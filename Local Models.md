- Vicki Boykis' walkthrough utilized Gemma 4 as the model of choice and LM Studio for the specific implementation
- The workflow gets defined in a Docker container
- Essential components
	- **Local model inference engine** (e.g., Ollama or LMStudio) to run an already trained model
	- **Agentic harness** (e.g., Claude Code or Pi) to act as an OS of sorts for the local inference engine
	- **Local model artifact** to document model weights and parameters
- The local model inference engine exposes the local model artifact, which the harness utilizes
- As a security measure, grant the Docker container permission to only run bash, not Python or web browsing
- User interaction workflow:
	1. Build the Docker container
	2. Make any necessary changes to files in the Docker container's repo
	3. Run Pi in the repo
	4. Pi spins up Docker, to avoid changes on actual files
	5. Pi sees the model json config within the container