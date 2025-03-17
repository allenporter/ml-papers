# Paper Reading

This page contains papers that I read, mostly from the "Top ML Papers of the Week"
substack as well as my summary notes to get a TL;DR of the paper.

## 2025-03-16

- [Gemma3](https://storage.googleapis.com/deepmind-media/gemma/Gemma3Report.pdf)
- [Transformers Without Normalization](https://arxiv.org/pdf/2503.10622)
  - LayerNorm looks like tanh. Dynamic tanh performs similar.
- [Auditing Language Models for Hidden Objectives](https://assets.anthropic.com/m/317564659027fb33/original/Auditing-Language-Models-for-Hidden-Objectives.pdf)
  - Techniques for safety evaluations

## 2025-03-09

- [The First Few Tokens Are All You Need](https://arxiv.org/pdf/2503.02875)
  - Rejection Fine Tuning improves accuracy but not coverage of reasoning traces
  - Unsupervised Prefix Fine Funing maximizes coverage of the reasoning trace
- [Forecasting Rare Language Model Behaviors](https://arxiv.org/pdf/2502.16797)
  - Techniques for forecasting risk for models in deployment
- [How Well do LLMs Compress Their Own Chain-of-Thought?](https://arxiv.org/pdf/2503.01141)
  - most questions have a well-defined ‘token complexity’
  - Token complexity alone can predict the performance of CoT prompting strategies with 95% accuracy

## 2025-01-26

- [Humanity's last exam](https://static.scale.com/uploads/654197dc94d34f66c0f5184e/Publication%20Ready%20Humanity's%20Last%20Exam.pdf?utm_source=substack&utm_medium=email)
- [Can LLMs Plan?](https://arxiv.org/pdf/2501.13545)
  - Can LLMs generate long-horizon plans that rival human performance without external
  tools?
  - If so, what key factors differentiate our prompting technique from other step-by-step methods like Chain-of-Thought?
- [Hallucinations Can Improve Large Language Models in Drug Discovery](https://arxiv.org/pdf/2501.13824)
  - Models can use halicunated inputs (especially from GPT-4o) to improve quality.
- [LLMs and Behavioral Awareness](https://arxiv.org/pdf/2501.11120)
  - Models can make statements about the policies they have been fine tuned with. "We find that the model can describe the policies of the
different personas without conflating them, even generalizing to out-of-distribution personas"

## 2025-01-19

### Enhancing Retrieval-Augmented Generation: A Study of Best Practices

Paper: [Enhancing Retrieval-Augmented Generation: A Study of Best Practices](https://arxiv.org/pdf/2501.07391)

- Good results from contrastive in context learning

### VideoRAG

Paper: [VideoRAG](https://arxiv.org/pdf/2501.05874)

- Including video content provides substantial wins
- Text descriptions does not add significant advantage on top of video content

## 2024-08-18

### RagChecker

[Paper](https://arxiv.org/pdf/2408.08067)

Approach for evaluating RAG systems

### EfficientRAG

[Paper](https://arxiv.org/pdf/2408.04259)

Multi-round retrieval with a smaller model, instead of multi-round LLM answering.

## 2024-07-08


### Searching for Best Practices in Retrieval-Augmented

[Paper](https://arxiv.org/abs/2407.01219)


### Scaling Synthetic Data Creation with 1,000,000,000 Personas


[Paper](https://arxiv.org/abs/2406.20094)

Notes:
- Text-to-Persona: Use the training data to create personas that may be searching for the text
- Persona-to-Persona: Generate other relations from the primary persona. e.g. primary is a nurse at a child hospital, then generate a child as another persona.
- Deduplication: Reducing duplicates of the billions of personas
  - MinHash to dedup text on n-grams
  - Embedding with `text-embedding-3-small` filter out personals with a cosine semantic similarity greater than 0.9.
- Then... Create a math problem for the persona.
- Results indicate that it is helpful to use the personas for creating diverse sets of data
- Examples of tool use and creating characters in a game.



### APIGen: Automated PIpeline for Generating

[Paper](https://arxiv.org/pdf/2406.18518)

Notes:
- Verifiable and Diverse Function-Calling Datasets
- Data generation pipeline that facilitates function calling
- Developed a dataset of 60k documents
- Stages of verification:
  - Format checker - syntax tests to make sure the data is properly formatted, ensures arguments are valid, etc.
  - Execution checker - test the output of actually runing the command. provides very fine grained error details if it does not succeed.
  - Semantic checker - Ask another LLM: does it make sense? was the desired result achieved? does the number of function calls make sense, are the results relevant.
- Berkeley function calling benchmark 




## 2024-06-30

### Improving Retrieval in LLMs through Synthetic Data

[Paper](https://arxiv.org/pdf/2406.19292)

Notes:

- Uses an answer template and only compute loss on the answers in the template. This lets the model focus on the retrieval task rather than how to answer the question
- Fine tuning did not hurt performance on other benchmarks


### LongRAG: Enhancing Retrieval-Augmented Generation with Long-context LLMs

[Paper](https://arxiv.org/abs/2406.15319)

Notes:

- Separate retrieval into a "long retirever" and a "long reader" that does the summarization of the answer.

## 2024-06-09

### AgentGym: Evolving Large Language Model-based Agents across Diverse Environments

[Paper](https://arxiv.org/pdf/2406.04151)

Notes:

- AGENTGYM is made from these contributions:
  - Platform for standardizing tasks/goals for agents. Exposed through HTTP services.
    - 14 environments, 89 tasks, available for expansion
  - Benchmarks & trajectories
    - [AGENTEVAL](https://huggingface.co/datasets/AgentGym/AgentEval): Base set of instructions and tasks
    - [AGENTTRAJ](https://huggingface.co/datasets/AgentGym/AgentTraj-L): Trajectory set
    - All collected using human annotations and expanded with models
  - Self-evolution investigation
    - AGENTEVOL - Novel method to explore agent evolution across environments.
    - Evolution is pronounced, comparable or better performance than SOTA models.


## 2024-03-31

### Agent LUMOS: Unified and Modular Training for Open-Source Language Agents

[Paper](https://arxiv.org/pdf/2311.05657.pdf)

Notes:

- Framework for training open-source LLM-based agents. 7B with high performance.
- Collect training annotations derived from ground-truth reasoning rationales
- Advantages:
  - Beats larger open source agents
  - outperforms opensource agents produced by chain-of-thoughts training
  - genearlizes to unseen tasks
- Modules:
  - Planning: decomposes a complex task into subgoals
    - Example: The device in her hand is from which country?
      1. Identify the brand of the device in her hand
      1. Answer the country of the brand
    - Actions are interpretable and tool-agnostic
    - Makes debuggign and learning new plans easier (independent of other modules)
  - Grounding: translates planning module subgoals into actions
    - Generates actions based on the plan
    - Actions can reference outputs of previous steps
  - Execution: Runs the actions
- Implemented w/ (1) One approach that generates the actions up front and (2) One
  approach that runs iteratively (adaptive)
- Converts ground truth for existing benchmarks into a unified format. Expect the data sources is generally useful.
- Training with converted annotations in multi-turn, loss of groudntruth responses (minus user prompt tokens)
- Outperforms other LLM Agent models by a large margin, as well as closed source models



## 2024-03-24


### What Are Tools Anyway?: A Survey from the Language Model Perspective

[Paper](https://zorazrw.github.io/files/WhatAreToolsAnyway.pdf)

Notes:

- Tools help with
  - Perception - e.g. time
  - Action - change environment
  - Computation - calculator or some other functions
- Agents use perception tools, and action tools.  Models that only use computation tools or do not act - with the environment are not called agents.
- Basic approaches
  - Inference time prompting: Approaches today use tools from input prompt
  - Learning by training
  - Tools are not yet useful for machine translation, summarization, and sentiment analysis
- For 5-10 tools, the LLM can pick from the list. Otherwise, need tool selection process
- Tools selection
  - As the # of tools grows, you need a special tool selection step:
    - Train separate tool selection modules
    - Use existing off the shelf embeddings for tools
  - Multi-tool use requirements 
    - Use intermediate contexts
    - May require iteration, parallel calls, or nested calls e.g. weather(get local time(‘Pittsburgh’)) 
- Evaluation
  - Existing datasets for other purpopses:
    - E.g. reasoninig
  - Full text answer comparison. Evaluations of these tool-augmented systems follow the standard    evaluation process for individual datasets
  - Aggregated API Benchmarks
    - Some are executable, some are not given the cost
    - Criteria:
      - Answer correctness
      - Which tool was used - measures planning
      - Reusability - sign of efficiency
    - What's missing?
      - Efficiency: costs of computation, teaching LMs to use them - can make comparisons more fair
      - Quality - Not just accuracy, but also quality. Memory usage, success rate/failure rate, etc
      - Reliability - VQA quality. Rule based tools don't have an issue here
      - Reproducible testing: Tools may not have static environments, therefore making a static evaluation benchmark with refernces answers is harder.
      - Evaluating the API calls without actually executing them i shelpful.
      - Also: Parallel testing running the model program and refernece program and comparing answers.
      - Safety/security evaluations

### RankPrompt: Step-by-Step Comparisons Make Language Models Better Reasoners

[Paper](https://arxiv.org/abs/2403.12373)
Notes:

- Out performs majority voting
- Higher cost than other methods given additional LLM calls

### RAFT: Adapting Language Model to Domain Specific RAG

[Paper](https://arxiv.org/abs/2403.10131)
Notes:

- Focus is on adapting pre-trained LLMs to a domain
- Methods for comparison:
  - "Closed book test" Bake in knowledge at train time 
  - "Open book test" RAG. Existing in-context retrieval methods are equivalent to taking an open-book exam without studying
  - RAFT - Aims to not only enable models to learn domain specific knowledge through fine-tuning, but also to ensure robustness against inaccurate retrievals.
- RAFT Approach
  - Dataset prep
    - Question (Q)
    - Set of documents (Dk)
        - Oracle document (D*). Can be more than one.
        - Distractor documents (Di)
    - Chain-of-thought style answer (A*) generated from one document D*
  - Training prep
    - For P fraction of questions (qi)
      - Retain the oracle document and distractors
    - For 1-P fraction of questions (qi)
      - We include no oracle document and only include distractor documents (dk).
    - Then use standard SFT approach
  - TL;DR: Effectively by removing the answers form the context, we're training 
    the model to memorize the answers instead of deriving them from context.
  - The chain-of-thought is a key factor in enhancing the quality
- Evaluation
  - Findings:  RAFT7B model (a finetuned version of LlaMA-2) is better at reading and extracting information from in-domain documents, than domain specific finetuned model, and general-purpose
model with RAG.
  - Evaluated on existing datasets (Natural Questions, PubMed, APIBench )
  - Comparison models:
    - Llama 7B zero shot
    - Llama 7B with RAG
    - Domain fine tuned zero shot
    - Domain fine tuned rag
- How much of the fine tuned corpus should be trained to include oracle documents? Paper used P=80%. Finding is that it depends on the dataset.
- Other studies look more generally at improving rag performance, but this looks only
  at documents in the same domain.


### Agent-FLAN: Designing Data and Methods of Effective Agent Tuning for Large Language Models

[Paper](https://arxiv.org/abs/2403.12881v1)
Notes:

- Goal is to make open source models perform as well as cloud models for agent tasks
- observations:
  1. typical training data is both format following and reasoning. Model seems to quickly learn the format, but may not be learning the content.
  1. different abilities are learned at different speeds
  1. existing approaches are ignoring hallucinations, focused on abilities. e.g. will call wrong tool or reply with tool use when no tools are aupplied.
- The approach is to split up the dataset and training process to account for 
  the difference in speeds of learned abilities and evaluate hallucinations
  with a new benchmark.
- Approach
  - Transform formatted data into natural conversations
  - Allows boosting pure agent capabilties independent of format
- Only a small portion of instruct following data is enough to achieve satisfying results.
