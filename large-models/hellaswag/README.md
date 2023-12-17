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

## First Attempt

The first attempt is to try zero-shot using a simple prompt like this:

```
Choose the most plausible continuation for the story.

Please answer with the letter of the correct answer.

Members of the procession walk down the street holding small horn brass instruments. A drum line
A) passes by walking down the street playing their instruments.
B) has heard approaching them.
C) arrives and they're outside dancing and asleep.
D) turns the lead singer watches the performance.
```

TL;DR: The accuracy wasn't very great.

### Mistral 7B Inst - mistral-7b-instruct-v0.1.Q4_K_M

  - ~40% on Swag dataset after 450 iterations. (+/- 4%)
  - ~42% on HellaSwag dataset after ~430+ iterations.
  - Question: Is this getting lower scores due to quantization? Could be worth
    trying a non-quantized model and comparing the quality.
  - Question: Would this model do worse in HellaSwag?

### Mistral 7B Inst - mistral-7b-instruct-v0.1.Q5_K_M

  - ~43% on HellaSwag dataset after ~430+ iterations.

### gpt 3.5 turbo
  - 53% on Swag dataset after ~315 iterations. I counted 5 more questions that could have been
    considered corret using the improvements described.

### Questions & Observations

- The current approach was very naive w.r.t. matching outputs. It was fairly
common to see lowercase vs uppercase mismatches or small grammar fixes (e.g.
the data had a typo and the LLM fixed it, or plural differences). These were not
common enough to be large factors, but enough that it could squeeze out a few
points. Possible improvements:
  - Testing for the simple result like `C)` could help.
  - Lowercase the answer/match
- These results are far lower than observed results. Is the prompt setup properly? The prompt was based on the Open AI LLM eval, however I didn't try that exact library. Could be worth checking an existing harness against the library.
- Is it zero shot vs 10-shot performance? From discussion in https://github.com/ggerganov/llama.cpp/discussions/2321 the prompt only gets a few points difference
- Looking at https://github.com/EleutherAI/lm-evaluation-harness it's not using the chat completion API. Maybe that is part of the problem.

## Second Attempt - 10 shot

This attempt tried some other approaches:
- Updated the prompt with 10 example answers
- Improved matching for answers containing the letter e.g. `C)`

Now the prompt is way larger (since it contains 10 question/answers instead of just one) and
so the performance on the GPU is around 15 queries per second.

This had a significant accuracy improvement.

### Mistral 7B Inst - mistral-7b-instruct-v0.1.Q4_K_M

  - ~66.29% on Swag dataset after ~250 iterations. (+/- 5.77%)
