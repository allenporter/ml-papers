# HellaSwag



My goal is to learn how to apply a common LLM benchmark to a few different models
basically to get an eval harness setup. It is not necessarily obvious to me how
LLMs are evaluated, so my hope is to read the paper from the dataset and
reproduce results from papers like LLaMa2 on these datasets.

The HellaSwag benchmark was designed to have questions that are difficult for
LLMs but easy for Humans. [HellaSwag: Can a Machine Really Finish Your Sentence?](https://arxiv.org/abs/1905.07830). Now, however, many LLMs approach or beat human accuracy.

The [SWAG](https://arxiv.org/abs/1808.05326) set was a prior dataset.

> Recall that models for our dataset take the following form: given a
> sentence and a noun phrase as context c = (s, n),
> as well as a list of possible verb phrase endings
> V = {v1, . . . , v4}, a model fθ must select a verb
> ˆi that hopefully matches igold:
> ˆi = argmax (i) fθ(s, n, vi)

We can simulate following the approach used by the open ai eval suite which is
to make a prompt that asks a multiple choice question and validates the answer.

The [Open AI Evals](https://github.com/openai/evals) is used as a reference.