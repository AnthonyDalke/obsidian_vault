### GPT Models

- GPT models actually only contain decoders, not encoders
	- Encoders *extract* info from text ("encode meaning"), while decoders *generate* text
- The GPT training sequence involves unsupervised pre-training first, then supervised fine tuning (SFT): "enhancing pre-trained models with more specific labeled info"
- After training, task-specific input transformation adapts outputs to the nature of the model's given task
	- Represents an architectural decision to adjust a model to a task "after the fact", rather than building specialized components
- Components of decoders
	- Text and position embed
		- Create "learned word embeddings" - vectors expressing meanings of words
		- Also create "learned positional encodings" - vectors conveying locations of words
	- Masked multi-head self-attention
		- Construct a matrix to capture the meaning of an input sequence, after considering combinations of word placements
	- Normalization layer
		- Scale the output
	- Feed-forward network
		- Another normalization layer
- Ultimately, GPT's take words from their outputs, concatenate them with the input text, and predict the next word in the output
- Foundation models get trained on a wide variety of data
	- After training, they can get applied to a variety of use cases
	- SFT can further specialize models
- Emergence refers to unintended consequences and use cases that arise as models grow in complexity and size
- Alignment consists of model and value alignment
	- Model = accuracy
	- Value = philosophical (safety)
- Alignment can occur in phases
	1. Pre-training on a broad dataset (weak alignment)
	2. SFT
		- Humans create validation datasets of expected outputs, which the model utilizes to re-train, still with the same or similar technical approach to training
		- Differs from generic fine-tuning, which aims to specialize a model for a particular domain or use case
		- In contrast, SFT tweaks a model's style, while preserving its general applicability
	3. Reinforcement Learning with Human Feedback (RLHF)
		- Follows an iterative loop, where human scorers review rounds of outputs
		- Models leverage Proximal Policy Optimization as an algorithm to tailor output to the human feedback, by maximizing cumulative rewards
- Positive prompting techniques generally work better than negative
- Prompt tuning involves tweaking model outputs through prompts, rather than SFT or RLHF, which require far greater resources

### Transformers
- Transformers introduced two key innovations:
	- Self-attention mechanism
	- Parallel processing of input data
- Transformer model architectures include:
	- Auto-encoding
	- Autoregressive
	- Sequence-to-sequence
- Attention directs focus to specific segments of input data
- RNN's handle natural language sequentially
	- Inputs get fed into the model and output get predicted in segments defined by timestamps
	- However, each output prediction does consider the full input sequence and outputs predicted up to that point
- RNN's struggle as input sequences grow
	- Also, their sequential nature hinders parallel scaling
- Attention address RNN shortcomings by enabling attention (hence, the name) on subsets of input sequences
	- The models calculate the relevance of other words in input sequences when considering a word in an input
- Unlike GPT models, transformers can feature both an encoder and decoder
	- Some varieties use only an encoder, while others use only a decoder
	- The encoder aims to "enhance" the input data, which the decoder then utilizes to produce outputs
- Models learn embeddings, both on input and output data, during training
- Positional encoding specifically enables parallel processing of input data
- Input embedding and positional encoding = meaning of a token + directional location of a word
	- These get combined, then represented as a matrix
- Steps building multi-head attention
	1. Create a query, key, and value (Q, K, V)
		- "Different representations of input data"
		- Created by training dense networks specifically for each component (Q, K, V)
	2. Divide Q, K, V into "multiple heads"
		- Different combinations of each get passed to different attention heads, with the count of heads configurable
	3. Feed the divided heads into the attention head
	4. Feed the output of the attention head to the final output
		- These combinations get assembled into matrixes, with dot products computed to calculate values of importance for words relative to one another
		- These matrixes become the attention matrix
		- The attention matrix then gets multiplied by the actual values in the dadta
		- These steps occur in each attention head
- Encoder and decoder components "add" and "norm" steps
	- "Add" re-introduces old data to keep output anchored to it
	- "Norm" involves scaling output values to smaller distribution ranges
- Outputs of multi-head attention get passed on via the feed-forward step
	- Ensures correct format
- Masked multi-head attention prevents data leakage, by "masking" later fragments of input sequences when training