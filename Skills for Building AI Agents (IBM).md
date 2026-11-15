1. System design
2. Tool and contract design
	- Contracts add elements of determinism ("I give you this input, and you return that output.")
3. Retrieval engineering
	- RAG comes into play here
	- Considerations include how to chunk information, how to manage embeddings, and re-ranking
4. Reliability engineering
	- Encompasses retries with back-off logic and timeouts
5. Security and safety
	- Risks to address include prompt injections, permissions, and boundaries
	- Address with impact validations, output filters, and permissions
6. Evals and observability
	- Tracing logs actions
	- Tests can avoid issues
	- Metrics measure performance
7. Product thinking