# New: use Claude Code

## Table of contents

- [Introduction](#Introduction)
  - [What is Claude Code](#What-is-Claude-Code)
  - [Compared to other harnesses and LLMs](#Compared-to-other-harnesses-and-LLMs)
  - [How prevalent is its use](#How-prevalent-is-its-use)
- [How to use](#How-to-use)
  - [How it works](#How-it-works)
  - [How students use it at school 42](#How-students-use-it-at-school-42)
  - [Personal experiences](#Personal-experiences)
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
Claude Code is more precise in following your instructions than Codex from ChatGPT/OpenAI but Codex can answer even when your prompt is vague. Else Codex is open-source while Claude Code is not, Codex as a harness but not ChatGPT as the LLM can be run locally. Py is open-source and very flexible, in that it is 100% modulable, but as a result harder to use. As it only is a harness, you can connect it to the LLM you want. Also you can run it for free with an open-sourced LLM on a local server like Ollama.

Some say Claude is superior for programming, analyzing or writing long texts, handling complex tasks, and in general within professional contexts. Gemini and chatGPT seem superior for deep web research or accessing real-time live data. But those models' responses can be customized, and then the quality of your prompt might matter more over which model you use.

Claude cannot be run locally. The risk of using non-local models is that you don’t know what those organizations do with your data. There are some stories of OpenAI stealing work from others for example or Anthropic giving conversations to the police for them to arrest users. DeepSeek v4.1 flash seems to be the best model for running locally. Running locally also doesn’t cost tokens, but it does cost the electricity and infrastructure. Right now to fully run DeepSeek v4.1 flash you would need 30k of infrastructure. You can then run it on a dedicated server and access it via your laptop. This is way too expensive, you can run smaller models on your laptop but those aren't well competent. In the future infrastructure prices will maybe lower but right now running a competent model locally is way too expensive, plus you would need to maintain/update it yourself. While DeepSeek v4.1 flash is only an LLM, they also created an associated free to run harness.

### How prevalent is its use
Prompt engineering and AI automation engineering are buzzwords that refer to engineers able to prompt or organize/connect AI models to accomplish a certain task. Those skills are in demand, and can even be a requirement for programming jobs. However, certain industries — such as in cancer treatments or at NASA — still want programmers to do everything manually and not use AI for the most precision.

## How to use

### How it works 
You can customize your Claude Code with markdown files. The LLM will read those and basically use them as context when answering your prompts. <br>
Every model has a maximum context window, this is a fixed number of tokens it can hold at once (system prompt + conversation history + any injected markdown files).<br>
Claude Code can be customized by two types of markdown files.<br>
\- The first type is a 'CLAUDE.md' placed in the project root. This file is always added to the context window. It explains what/how to do. For example you can ask the LLM here to code a certain way such as using async/await or to be pedagogical by always explaining code.<br>
\- The second type are 'skills'. Each skill is a folder (with a name that identifies the skill) containing a 'SKILL.md' file, and optionally supporting files (references/, scripts/, assets/, templates/). Skill files define a concept or action that can appear in the prompt; for example when I say X it means I ask the LLM to do Y with Z inside A. I think built-in skills exist, or you can find pre-written skills online like plugins, else you might be able to ask an LLM to write the skill for what you want. An example of a custom skill: a 'pr-review' skill that defines your company's specific code review checklist (naming conventions, required test coverage, security checklist items), so instead of restating "review this PR the way we do it" every time, you can just ask "review this PR" and the skill's stored checklist gets pulled in automatically. At first, only the skill's name and short description of when the skill should be used are loaded into the context window, this costs little tokens. But when a skill is relevant to the prompt, the full 'SKILL.md' is added to the context window, and supporting files only if necessary.<br>
While 'CLAUDE.md' gets loaded into context each time, a skill only gets loaded when relevant. Thus skills allow you to spare certain tokens when they are not necessary. This makes you less likely to attain the context window limit, but also makes each request faster and cheaper, plus limits signal dilution (adding irrelevant instructions makes it harder for the LLM to locate the one instruction that is actually relevant).

You can even generate the code of a whole project simply by explaining in markdown files what needs to be done (we call this 'spec-driven-development'). 'Spec' refers to a document that describes in natural language what you want to be done. The 'wayfinder' skill is open-source and will help you find all the steps necessary for what you want to accomplish and thus help write your 'spec'.<br>
You can place different agents in different directories so that they each have their own instruction markdown files. For example one directory will be responsible for testing, another one for the frontend of the code, and so forth... 

Claude Code can also work alone in a loop until a certain goal is accomplished. For example you can ask it to generate code, generate tests, execute those tests, adapt the code based on tests results, test again, and so forth...

To use Claude Code you at least need a €20 subscription. This gives you a certain amount of tokens that should be enough unless you use it a lot on large projects. Once you have a subscription, you can follow the instructions [here](https://code.claude.com/docs/en/overview) to use Claude Code.

### How students use it at school 42 
While generating your whole project with Claude Code is technically allowed, the rule is always that you must understand your code. The correction file now asks students to explain code more or even to make live adaptations.

The student _rperez-t_ gives Claude Code the 42 school project subject, correction file, and the project code itself, and prompts/asks CLaude to correct the project and find discrepancies between the subject and project code. He sometimes uses chatGPT to create a good prompt for Claude.<br>
When asking Claude to code new features he will verify and ask Claude not to use too complicated code but instead use understandable code.

Newer students primarily use Claude within their terminal to get explanations about code or to generate tests. They can use a 'CLAUDE.md' that says Claude should only be used pedagogically to understand how to code and not to just generate code.

Another student uses Claude within VSCode and gives him precise instructions to build new features such as what function to build in what file. He doesn't use 'skills' or 'CLAUDE.md' for Claude. While those can be very useful, they are more so advanced features who are not necessary to set up for simple use.

### Personal experiences
It is very simple to use. Simply launch it in your terminal with `claude` and afterwards ask your questions in natural language like you would any LLM, subsequently Claude Code will give clear answers with clear propositions of what to do next (which you can accept or not (by using tab you can specify more with a comment what you want) and he will execute the task and propose subsequent tasks himself). Those subsequent tasks can be tests he does to afterwards refine his code until the code works perfectly. Sometimes I prefer to test myself when I think the code is good to avoid wasting tokens, else it is useful to let him test so he can react to the test outputs.

He knows your whole project code when you ask a question and is very effective at determining what needs to change in it. Not only that, he also executes changes for you and can add large amounts of code.

As of now he has been highly useful for me to adapt old projects I don't know anymore, and this without me even needing to customize it with markdown or skill files. For example he also prepared tests and corrected them for a large project in hours which would otherwise have taken me weeks (if not be impossible for me). Claude Code was even able to: test and rectify memory leaks and invalid read/write; launch docker (as long as docker runs on your computer) to test the project in a linux environment and rectify it as needed; but also explain how to use a project in the README.

Sometimes chatGPT cannot resolve a problem but Claude Code can, this may in part be due to Claude Code having access to more information but it might also just be Claude being more intelligent.

## References
Learned from 42 Belgium student _edesmed_, _rperez-t_, and briefly others.
