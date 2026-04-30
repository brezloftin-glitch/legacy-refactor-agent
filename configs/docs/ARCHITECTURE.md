# System Architecture

## 1. DAG (Directed Acyclic Graph) Generation Logic
The Decision Agent relies on a custom topological sorting algorithm to convert the AST dependencies into a DAG. 
This ensures that the Refactoring Agent always starts from the *Leaf Nodes* (classes with zero outgoing dependencies) and moves upwards to the *Root Nodes* (controllers/API layers). 

This approach completely eliminates the "contextual hallucination" where an LLM attempts to use methods from dependencies that have not yet been modernized.

## 2. Self-Healing Loop Mechanism
When the `Execution Agent` outputs refactored code and Mockito tests, the `Validation Agent` triggers a Maven build in an isolated Docker container. 

If a `CompilationError` or `AssertionError` occurs:
1. The error stack trace is extracted using Regex.
2. The exact line of failure is mapped back to the LLM's generated response.
3. A strict prompt is constructed: `[SYSTEM] Your previous refactoring failed. Error logs: <LOGS>. Fix the implementation focusing on line <LINE_NUM>.`
4. This loop iterates a maximum of 3 times before graceful degradation (human intervention).

## 3. Why MiMo-V2.5-Pro is Critical
Currently, large legacy classes exceed standard 128k context windows when combined with their dependency interfaces and tests. Chunking these files breaks semantic relationships. By migrating to MiMo-V2.5-Pro (1M context), we aim to inject the entire module AST and source code simultaneously, achieving a 100% zero-shot architectural transformation.
