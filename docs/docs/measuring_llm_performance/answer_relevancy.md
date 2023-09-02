# Answer Relevancy

We provide a simple interface for ensuring question-answering relevancy powered by the cosine similarity between bi-encoder QA models. This is important when you have ground truths and LLM outputs and you want to make sure they have the same concepts. 

For example - when asked:

How big is this apple?
- 12 square feet
- The size of an orange

While they are both relevant and may not be hallucinating - it's important to note that they are conceptually different ways of answering.

## Assert Answer Relevancy

```python
from deepeval.metrics.answer_relevancy import assert_answer_relevancy
query = "What is Python?"
answer = "Python is a programming language?"
assert_answer_relevancy(query, output=answer, minimum_score=0.5)
```

### Parameters

- `minimum_score` refers to the minimum score for this to be considered relevant

## Answer Relevancy As A Metric

If you would instead like a score of how relevant an answer is to a query, simply call the metric class.

```python
from deepeval.metrics.answer_relevancy import AnswerRelevancy
scorer = AnswerRelevancy(minimum_score=0.5)
scorer.measure(query=query, output=answer)
# Returns a floating point number between 0 and 1
```

### Parameters

- `minimum_score` refers to the minimum score for this to be considered relevant

## How It is Measured

Answer relevancy is measured using DL models that are trained off MS-Marco dataset (which is a search engine dataset). The method to measure relevancy is that it encodes a query and an answer and then measures the cosine similarity. The vector space has been trained off query-answer MSMarco datasets to ensure high similarity between query and answer.