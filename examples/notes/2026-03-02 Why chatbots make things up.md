---
date: 2026-03-02
source: Example Tech Weekly (fictional)
concepts: ["[[Large language model]]", "[[Hallucination]]", "[[Next-token prediction]]"]
---
# Why chatbots make things up

A large language model writes by predicting the next word again and again. It has no built-in
check against a database of facts, so when it lacks information it still produces a fluent,
confident answer — a "hallucination". Giving the model the source document in the prompt
(retrieval) cuts the error rate a lot but not to zero. The article recommends asking the model
to quote the part of the source it relied on.

## My notes
