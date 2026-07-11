# New: use Claude Code

## Table of contents

- [Introduction](#Introduction)
  - [What is Claude Code](#What-is-Claude-Code)
  - [Compared to other harnesses and LLMs](#Compared-to-other-harnesses-and-LLMs)
  - [How prevalent is its use](#How-prevalent-is-its-use)
- [How to use](#How-to-use)
  - [How it works](#How-it-works)
  - [How students use it at school 42](#How-students-use-it-at-school-42)
- [References](#References)

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

### How it works 
You can customize your Claude Code with markdown or skill files. The LLM will read those and basically use them as context when answering your prompts. <br>
Markdown files explain "what". For example you can explain in a 'Claude.md' file what you want Claude to do — for example if you want it to only be pedagogical by explaining code.<br> 
Skill files explain "how to". You can explain concepts inside a skill file, for example when I say X it means I ask Claude to do Y with Z inside A. It is like text replacement where a word in your prompt becomes a whole explanation of how to do it.

You can even generate the code of a whole project simply by explaining in markdown files what needs to be done and in skill files how so. You can place different agents in different directories so that they each have their own instruction files (markdown and skills files). For example one directory will be responsible for testing, another one for the frontend of the code, and so forth... 

Claude Code can also work alone in a loop until a certain goal is accomplished. For example you can ask it to generate code, generate tests, execute those tests, adapt the code based on tests results, test again, and so forth...

To use Claude Code you at least need a €20 subscription. This gives you a certain amount of tokens that should be enough unless you use it a lot on large projects. Once you have a subscription, you can follow the instructions [here](https://code.claude.com/docs/en/overview) to use Claude Code.

### How students use it at school 42 
While generating your whole project with Claude Code is technically allowed, the rule is always that you must understand your code. The correction file now asks students to explain code more or even to make live adaptations.

The student _rperez-t_ gives Claude Code the 42 school project subject, correction file, and the project code itself, and prompts/asks CLaude to correct the project and find discrepancies between the subject and project code. He sometimes uses chatGPT to create a good prompt for Claude.<br>
When asking Claude to code new features he will verify and ask Claude not to use too complicated code but instead use understandable code.

Newer students primarily use Claude within their terminal to get explanations about code or to generate tests. They can use a README (Claude.md) that says Claude should only be used pedagogically to understand how to code and not to just generate code.

Another student uses Claude within VSCode and gives him precise instructions to build new features such as what function to build in what file. He doesn't use _Skills_ or _READMEs_ for Claude. While Skills and READMEs can be very useful, they are more so advanced features who are not necessary to set up for simple use.

## References
Learned from 42 Belgium student _edesmed_, _rperez-t_, and briefly others.
