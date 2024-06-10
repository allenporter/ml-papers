# Paper Reading

This page contains papers that I read, mostly from the "Top ML Papers of the Week"
substack as well as my summary notes to get a TL;DR of the paper.

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
