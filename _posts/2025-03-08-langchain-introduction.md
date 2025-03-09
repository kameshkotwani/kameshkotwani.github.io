---
layout: single
title: "Not your lame LangChain Introduction"
date: 2025-03-08
categories: [Machine Learning,Langchain, OpenAI, LLMs, Agents]
tags: [langchain,chatgpt,claude,gemini,llm-agents]
author_profile: true
read_time: true
comments: true
share: true
related: true
toc: true
toc_sticky: true
---
[LangChain](https://www.langchain.com/langchain) is an open-source framework for developling applications powered by large language models (LLMs). This article covers the theoretical aspect of LangChain by building a fundamental block for the challenges that a developer can face when creating something complex as a chat application, notably using custom data, and how Langchain comes into the picture to integrate, automate, and produce a complex chat application for seamless integration with multiple LLMs such as OpenAPI, Gemini, Huggingface, and many more.

## Why do we need Langchain

Before starting off with the introduction and technical aspect, we should first know what the need of Langchain is. Let's suppose you have a huge compilation of books and would like to create an application using which you could dump all your PDFs and literature and ask any question you want in the world.
Example queries can be:

This high-level image tells us that we have built an application which is combination of books through which user can ask any question.

![Langchain Image]({{ site.url }}{{ site.baseurl }}/assets/images/langchain-images/langchain1.png)

- Explain page number 5 like I am five.
- Generate True or False questions for my exam
- Generate small notes which I can use to cheat in my exam

Ah, you get the idea.

### Building a text application for user interaction

So let's design the application as is. But before that, we need to implement a system design for such a complex application.

#### System Design

![High Level Design]({{ site.url }}{{ site.baseurl }}/assets/images/langchain-images/langchain2.png)
