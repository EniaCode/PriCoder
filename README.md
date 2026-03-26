# Fix AI-generated code that breaks on your internal APIs
## TL;DR
AI-generated code still breaks on internal APIs — even when the model sees the full API documentation.

PriCoder makes your API calls actually work.

→ Correct API calls  
→ Fewer runtime errors  
→ Code that actually runs

## Try it in your IDE
See broken API calls fixed in your own codebase.
1. Install the plugin  
2. Open your project  
3. Ask AI to modify or generate code using your internal APIs  
- Install [Enia Code](https://www.eniacode.com) plugin
- View [docs](https://www.eniacode.com/docs)

## Where it breaks
Looks correct. Still wrong.

The model sees the API — but fails to follow required usage patterns:
##### ❌ LLM output (with API access)

```python
import ndonnx

def safe_ratio(x, y):
    result = ndonnx.divide(x, y)              # missing asarray
    return ndonnx.where(y == 0, 0.0, result)      # incorrect API usage
```
##### ✅ correct usage

```python
import ndonnx

def safe_ratio(x, y, fallback=0.0):
    x = ndonnx.asarray(x)
    y = ndonnx.asarray(y)

    quotient = ndonnx.divide(x, y)
    return ndonnx.where(y == 0, fallback, quotient)
```
The model sees the APIs — but still fails to invoke them correctly, even with full API specifications.

## What PriCoder does
PriCoder trains models on how APIs are actually used in real code.
- learns API invocation patterns, not just documentation
- improves multi-step API usage
- reduces incorrect or missing API calls in real code

## Why it works
Most approaches (RAG):
- retrieve API documentation
- rely on models to use it correctly
## PriCoder:
- trains on how APIs are actually invoked
- learns usage patterns from synthesized execution-validated data
- improves API usage, not just API awareness

## Results
Even with full API documentation, models still fail on API-heavy code generation.

Baseline performance is low — pass@1 only improves from ~8% to ~13% with oracle API specs.

PriCoder significantly improves this:
- +20%+ absolute pass@1 improvement  
- higher success rates in multi-call workflows  
- fewer runtime execution failures

These gains come with negligible impact on general code generation.
(See [paper](https://arxiv.org/abs/2603.15159) for full evaluation details)

## Paper
[To See is Not to Master: Teaching LLMs to Use Private Libraries for Code Generation](https://arxiv.org/abs/2603.15159)

## Notes
PriCoder focuses on a core gap in current AI coding systems:

Models can see APIs, but don’t know how to use them.

This project addresses that gap.

Feedback and discussions are welcome.

## Local Pipeline
Run the main PriCoder pipeline:

```md
```bash
cd data_generation
cd ../api_extract
cd ../benchmark_generation
cd ../infer_and_eval
```
Optional steps:
- pypi_crawling/: collect and filter package/API sources 
- data/: contains reusable datasets (documents and benchmarks)
