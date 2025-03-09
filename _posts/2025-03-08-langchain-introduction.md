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
auto_ids: true
toc_levels: 1..6
toc_icon: 'book-open'
---
LangChain[^1] is an open-source framework for developling applications powered by large language models (LLMs). This article covers the theoretical aspect of LangChain by building a fundamental block for the challenges that a developer can face when creating something complex as a chat application, notably using custom data, and how Langchain comes into the picture to integrate, automate, and produce a complex chat application for seamless integration with multiple LLMs such as OpenAPI, Gemini, Huggingface, and many more. I humbly request you to read this article cover to cover, after reading you will have a solid answer to the question you see below.

## 1. World before LangChain

Before starting off with the introduction and technical aspect, we should first know what the need of Langchain is. Let's suppose you have a huge compilation of books and would like to create an application using which you could dump all your PDFs and literature and ask any question you want in the world.
Example queries can be:

This high-level image tells us that we have built an application which is combination of books through which user can ask any question.

![Langchain Image]({{ site.url }}{{ site.baseurl }}/assets/images/langchain-images/langchain1.png)

- Explain page number 5 like I am five.
- Generate True or False questions for my exam
- Generate small notes which I can use to cheat in my exam

Ah, you get the idea.
So lets discuss the design of this application without using LangChain.

## 2. No LangChain chat application

So let's design the application as is. But before that, we need to implement a system design for such a complex application.

### 2.1. Birds Eye view

![High Level Design]({{ site.url }}{{ site.baseurl }}/assets/images/langchain-images/langchain2.png)
Let's suppose as a user you ask a question from your system "What are the assumptions for Linear Regression", now based on the data you have provided in this current situation, we have a corpus of PDFs, stored in some database, and this design will take that query and perform a "semantic search" based on the database and will return the relevant pages (in this case the pages containing the information regarding the question we asked) and then create a `"system query"` and this will be transferred to the BRAIN (which is not yet disclosed as how it works and what it is, we discuss this later). Here our BRAIN is crafted in such a way that it has the capability of Natural Language Understanding such that it understands our query. Secondly, it should have "context-aware" text generation ability to create the answer. Finally, our BRAIN gives out the answer to the original question the user asked or in this case, we asked.

This design further raises questions, what is **semantic search**? And more importantly, why are we using it when we can directly feed the whole document to the BRAIN and get the answer anyway? So lets suppose the document we have is of thousand pages and we have a doubt in some topic "Linear Regression" which is present in page 462. Now, there are two ways we can approach this

- **Approach 1:** Go to our mentor hand over the book and ask that we doubt this topic.

- **Approach 2:** Go to the same mentor state the page number and ask the question.

Obviously, `approach 2` is better since our mentor can directly look into the problem and clear the doubt right away.
The same scenario works for our app as well. If we hand over the whole document, it will be computationally expensive and the results will be sub-par.

This is where the **semantic search** comes into play. But what is semantic search anyway? Well, here is your answer

### 2.2. Type of searches  

There are many types of searches which can be performed some of which we are interested in are:

#### 2.2.1. Keyword Search

**Keyword search** in documents helps find relevant information by matching search terms with words in the text. For example, searching "LangChain memory" in a documentation file will return sections where both words appear. However, it has drawbacks—it only works for exact matches, so "LangChain recall" might not show the same results even if the context is similar. It also fails with synonyms and doesn’t understand intent, making it less effective for complex queries. More advanced methods like semantic search address these limitations by understanding meaning, not just keywords.

#### 2.2.2. Semantic Search

**Semantic search** improves on keyword search by understanding the meaning and intent behind a query, rather than relying on exact word matches. Unlike keyword search, which only finds documents containing the exact terms, semantic search can retrieve relevant results even if different words are used. For example, searching "LangChain recall" would still return results about "LangChain memory", recognising that both are related concepts. This makes it more effective for handling synonyms, natural language queries, and context-aware retrieval.

_This is the reason why we are using semantic search rather than keyword search._

### 2.3. System Design

Let's dive deep into the actual architecture of the application and understand the complexity of creating such a beautiful and simple yet extremely complex chat application without the knowledge of LangChain. Open the image in new tab to see the beauty of it.

<figcaption> Architecture Desgin</figcaption>
![Langchain Image]({{ site.url }}{{ site.baseurl }}/assets/images/langchain-images/langchain3.jpeg)



## References

[^1]:<https://www.langchain.com/langchain>
