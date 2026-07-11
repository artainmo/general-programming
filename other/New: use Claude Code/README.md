# New: use Claude Code

## Introduction

### What is Claude Code
Claude Code is an AI-powered coding assistant that helps you build features, fix bugs, and automate development tasks. It reads your codebase, edits files, runs commands, and integrates with your development tools (available in your terminal, IDE, desktop app, and browser).

Claude Code is like having a really smart helper who lives inside your terminal (or IDE...). You tell it what you want in plain words — “make a website,” “add a login page,” “what does this code do?” — and it goes and does it. It reads your files, writes code, runs commands, and even tests things, all by itself.<br>
Think of it like this: normal Claude (in chat) is like texting a smart friend. Claude Code is like that same friend sitting at your computer, hands on keyboard, actually doing the work while you watch and approve.<br>
The key differences from Claude chat: it runs in your terminal, not in a browser; it can see your whole project — all the files, the git history, everything; it can run commands — install packages, run tests, commit code; you stay in control — it asks before doing anything destructive.<br>
So instead of copying code from a chat window and pasting it into your editor, Claude Code just does it directly.

In technical terms, Claude Code is the agentic harness built around Claude. While Claude itself is just a language model designed to predict text and reason about code, the harness provides the necessary tools, context management, and execution environment to turn it into a capable coding agent.<br>
While the model decides what to do, the harness executes the tools (like opening files or running tests), and feeds the result back in the model. This means the model is the "brain", while the harness provides the "hands".<br>
Unlike basic chatbots that strictly answer questions, agents can break down complex tasks, use digital tools, and work without human supervision. AI agents contain: LLMs; tools (like APIs, web search functions, calendars, or databases, allowing interactions with software environment); memory (enabling them to recall past interactions and maintain context throughout multi-step workflows). Claude code can thus be considered an agent.

### Compared to other harnesses and LLMs
Claude Code is more precise in following your instructions than Codex from ChatGPT but Codex can answer even when your prompt is vague, also Codex is open-source while Claude Code is not. Py is open-source and very flexible — in that it is 100% modulable — but harder to use. As it only is a harness, you can connect it to the LLM you want. Also you can run it for free with an open-sourced LLM on a local server like Ollama.

Some say Claude Code is superior for programming, analyzing or writing long texts, handling complex tasks, and in general within professional contexts. Gemini and chatGPT seem superior for deep web research or accessing real-time live data. But those models' responses can be customized, and then the quality of your prompt might matter more over which model you use.

### How prevalent is its use
Prompt engineering and AI automation engineering are buzzwords that refer to engineers able to prompt or organize/connect AI models to accomplish a certain task. Those skills are in demand, and can even be a requirement for programming jobs. However, certain industries — such as in cancer treatments or at NASA — still want programmers to do everything manually and not use AI for the most precision.

## How to use

### How students use it at school 42 
_rperez-t_ Le sujet, le correctif, et le projet, prompt (demander à chatGPT comment faire le prompt qui doit être pour Claude)...
Newer students 
Other student (wdeltenre)

### How it works to build a project from scratch
README files explain what... Skills explains how to in a file... You can place different agents (LLM with harness (context for LLM, code qui fait tourner le LLM d'une certaine manière)) in different folders so that they each have their own instruction files... You can create an agent that generates tests and executes the tests at the end... Afterwards it can correct the code and retest in a loop... 

## References
Learned from 42 Belgium student _edesmed_ and _rperez-t_.
