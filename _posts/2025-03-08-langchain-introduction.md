---
layout: single
title: "Not your lame LangChain Introduction"
date: 2025-03-10
show_date: true
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
LangChain[^1] is an open-source framework for developing applications powered by large language models (LLMs). This article covers the theoretical aspect of LangChain by building a fundamental block for the challenges that a developer can face when creating something complex as a chat application, notably using custom data, and how Langchain comes into the picture to integrate, automate, and produce a complex chat application for seamless integration with multiple LLMs such as OpenAPI, Gemini, Huggingface, and many more. I humbly request you to read this article cover to cover, after reading you will have a solid answer to the question you see below.

## 1. World before LangChain

Before starting off with the introduction and technical aspect, we should first know what the need of Langchain is. Let's suppose you have a huge compilation of books and would like to create an application using which you could dump all your PDFs and literature and ask any question you want in the world.
Example queries can be:

This high-level image tells us that we have built an application which is combination of books through which user can ask any question.

![Langchain Image]({{ site.url }}{{ site.baseurl }}/assets/images/langchain-images/langchain1.png)

- Explain page number 5 like I am five.
- Generate True or False questions for my exam
- Generate small notes which I can use to cheat in my exam

Ah, you get the idea.
So let's discuss the design of this application without using LangChain.

## 2. No LangChain chat application

So let's design the application as is. But before that, we need to implement a system design for such a complex application.

### 2.1. Birds Eye view

![High Level Design]({{ site.url }}{{ site.baseurl }}/assets/images/langchain-images/langchain2.png)
Let's suppose as a user you ask a question from your system "What are the assumptions for Linear Regression", now based on the data you have provided in this current situation, we have a corpus of PDFs, stored in some database, and this design will take that query and perform a "semantic search" based on the database and will return the relevant pages (in this case the pages containing the information regarding the question we asked) and then create a `"system query"` and this will be transferred to the BRAIN (which is not yet disclosed as how it works and what it is, we discuss this later). Here our BRAIN is crafted in such a way that it has the capability of Natural Language Understanding such that it understands our query. Secondly, it should have "context-aware" text generation ability to create the answer. Finally, our BRAIN gives out the answer to the original question the user asked or in this case, we asked.

This design further raises questions, what is **semantic search**? And more importantly, why are we using it when we can directly feed the whole document to the BRAIN and get the answer anyway? So let's suppose the document we have is of thousand pages and we have a doubt in some topic "Linear Regression" which is present in page 462. Now, there are two ways we can approach this

- **Approach 1:** Go to our mentor hand over the book and ask that we doubt this topic.

- **Approach 2:** Go to the same mentor state the page number and ask the question.

Obviously, `approach 2` is better since our mentor can directly look into the problem and clear the doubt right away.
The same scenario works for our app as well. If we hand over the whole document, it will be computationally expensive and the results will be sub-par.

This is where semantic search plays a crucial role. But what exactly is it? Well, here is your answer

### 2.2. Type of searches  

There are many types of searches which can be performed some of which we are interested in are:

#### 2.2.1. Keyword Search

**Keyword search** in documents helps find relevant information by matching search terms with words in the text. For example, searching "LangChain memory" in a documentation file will return sections where both words appear. However, it has drawbacks—it only works for exact matches, so "LangChain recall" might not show the same results even if the context is similar. It also fails with synonyms and doesn’t understand intent, making it less effective for complex queries. More advanced methods like semantic search address these limitations by understanding meaning, not just keywords.

#### 2.2.2. Semantic Search

**Semantic search** improves on keyword search by understanding the meaning and intent behind a query, rather than relying on exact word matches. Unlike keyword search, which only finds documents containing the exact terms, semantic search can retrieve relevant results even if different words are used. For example, searching "LangChain recall" would still return results about "LangChain memory", recognising that both are related concepts. This makes it more effective for handling synonyms, natural language queries, and context-aware retrieval.

_This is the reason why we are using semantic search rather than keyword search._

### 2.3. System Design

Let's dive deep into the actual architecture of the application and understand the complexity of creating such a beautiful and simple yet extremely complex chat application without the knowledge of LangChain. Open the image in new tab to see the beauty of it.

<figcaption> Architecture Design</figcaption>
![Langchain Image]({{ site.url }}{{ site.baseurl }}/assets/images/langchain-images/langchain3.jpeg)

At first glance, by looking at this design, if we go in simple terms, the workflow works something like this,
The user has a corpus which is stored in any cloud storage we please AWS or Azure Blob Storage, and this collection of PDFs is loaded using a "Document Loader" for splitting purposes. After that, the documents are split into pages using "Text Splitter" and converted into embeddings (which is just a fancy way of describing a representation vector which contains the text but in numerical form which a machine understands)[^2]. Popular services include Amazon Bedrock[^3].

To give a simple example, to understand what exactly is an embedding, let's say we have the text _"I am the one who knocks."_  This text will be represented into an embedding in an n-dimensional vector like this `[0.02,0.55,1.455,0.44.,.....,-0.555]`.

By this logic, every sentence, every page, and every word can be transformed into an embedding depending on the use case. But, creating an embedding every time a user inputs a query will be extremely bad system design and computationally expensive, so what do we do? Simple, we store them in a database. Some of the popular choices include Pinecone, Weaviate and more[^4].

![Langchain Image]({{ site.url }}{{ site.baseurl }}/assets/images/langchain-images/langchain5.png)

Now, we are at a point where we have created our own embeddings database which we can now use to perform semantic searches. But this is all from a builder's perspective.

From a user point of view, all we have to do is ask our query, which will be then converted into embeddings that we looked into just now, and then using semantic search, the relevant documents will be fetched from the database which we created earlier and then these relevant documents (containing the semantic meaning of the words, not just the word search) will be sent off to create a "System Query" (which is again a combination of the user query and the relevant pages which we just fetched) and then these will be passed to the "BRAIN" which has NLU  and Text generation capabilities to process and generate an answer to our query and return a response which will make the user happy!

![Langchain Image]({{ site.url }}{{ site.baseurl }}/assets/images/langchain-images/langchain6.png)

I hope I was able to explain the low-level design. Seems easy enough in today's world, but let's go through some of the challenges that we will face with this method:

#### 2.3.1. Challenge 1

The number one challenge here in our app is to create our BRAIN (our first component), which is capable of generating text given the query understanding it and it can generate relevant text. And guess what this text generation got its first breakthrough from one of the most famous papers in NLP "Attention is All You Need"[^5]. Then came BERT and GPTs and finally what we know today as LLMs. If you guessed it, you are right, drum rolls...... the BRAIN here is none other than Large Language Models (LLMs) which are quite a buzz currently.

_Today we can easily solve the first component challenge using LLMs._

#### 2.3.2 Challenge 2

Another challenge is to incorporate these LLMs, which are extremely large scale, deep-seek r1[^6] having 671 billion parameters which is 400GB in size. As a user, you cannot just download these models and use them as they are computationally expensive and even the world's most powerful personal computer cannot handle them plus it is not economical. So, what do we do? Absolutely nothing! Why? Because this challenge is also solved for us by companies such as OpenAI and Microsoft. They identified this problem and served these LLM models into their servers have provided us APIs to interact with them.  

![Langchain Image]({{ site.url }}{{ site.baseurl }}/assets/images/langchain-images/langchain4.png)

_So to create the app, we will be using LLM API, which gives us the advantage of only paying for what we use and is economical and computationally inexpensive as well. Finally our BRAIN here is the LLM API._

#### 2.3.3 Challenge 3

The third challenge we will face is orchestrating these components, if you look at the architecture design you might be able to point out the massive components we will have to handle including
Cloud Storage (AWS, Azure)
Document Loader
Text Splitter service
Embedding generation using models
Database to store embeddings
LLMs
So we have got so many tasks to perform document loading, embedding generation to talking to the LLMs for which we will need to create a robust pipeline to create all these components and handling the codebase to create these components will be extremely challenging and hectic and time-consuming. Even though you do manage to work through all of this, one day we might think that we do not need to use OpenAI components, rather we need to use Claude or any other LLM API for that matter. Changing this whole pipeline will cost you alot along with handling another codebase and lots of changes to make the pipeline compatible with other LLMs. Similarly you might want to use other storage solution, another model to create embedding, all of this will be extremely challenging.

## 3. Solution: LangChain

This is where LangChain comes into the play, the third challenge which is extremely complex to solve, is solved by the famous library. It gives you the plug-and-play functionality to change just some codebase and change your entire system sometimes even with just one line of code. So you want to change your provider from OpenAI to Google Gemini, just change your `API` key and change the `Class` and you are done! Similarly, you can change the entire infrastructure of your pipeline with just a little code change. And this gives you the power of not only focusing on your idea but also gives relief of not worrying about the backend of the services. It provides a streamlined way of communicating with your application in a powerful yet simple way using LLMs.

### 3.1. Benefits

LangChain offers a range of benefits that make it a powerful framework for building applications powered by large language models. Instead of manually orchestrating multiple components like document loaders, vector databases, and LLM integrations, LangChain provides a seamless and modular approach. Below is a summarised table outlining the key advantages of using LangChain:

| **Feature**          | **Benefit**  |  
|----------------------|-------------|  
| **Modular & Composable**  | Build reusable and flexible AI components.  |  
| **LLM Integration**  | Easily switch between OpenAI, Gemini, Claude, etc.  |  
| **Memory Management**  | Retain conversation history for chatbots.  |  
| **Semantic Search & RAG**  | Fetch relevant data instead of sending entire docs to LLM.  |  
| **Prompt Engineering**  | Optimise, manage, and version prompts.  |  
| **Multi-LLM Support**  | Use different LLMs for various tasks.  |  
| **Asynchronous Processing**  | Handle multiple user requests efficiently.  |  
| **Cross-Platform Support**  | Works with Python and JavaScript.  |  

Each of these features helps developers streamline their workflow, **reduce complexity**, and **enhance efficiency** when building intelligent applications. Whether you're developing a chatbot, a retrieval-based system, or an AI-powered assistant, LangChain makes the process more **scalable and adaptable**.

## 4. LangChain Flexibility: Switching LLMs & Embedding Models

One of LangChain’s biggest strengths is how easily you can swap components which we discussed as how code hectic they can be.

Using a simple code demonstration we can see how easily we can replace OpenAI’s GPT-4 with Google’s Gemini Pro and OpenAI’s embeddings with Hugging Face’s BAAI/bge-large-en model—all with minimal changes.

In this example we are using OpenAI to load GPT-4 model and generate embeddings and Meta FAISS to store the vectors and retrieve relevant information.

```python
from langchain.llms import OpenAI
from langchain.chains import RetrievalQA
from langchain.vectorstores import FAISS
from langchain.embeddings.openai import OpenAIEmbeddings
from langchain.document_loaders import TextLoader

# Load and process documents
loader = TextLoader("data/sample.txt")  
docs = loader.load()

# Convert documents into vector embeddings
vectorstore = FAISS.from_documents(docs, OpenAIEmbeddings())

# Create a retrieval-augmented QA system
qa_chain = RetrievalQA.from_chain_type(llm=OpenAI(model_name="gpt-4"), retriever=vectorstore.as_retriever())

# Ask a question
query = "What is LangChain?"
answer = qa_chain.run(query)
print(answer)

```

But what if you don’t want to pay OpenAI for their API, or your company decides to switch to another provider? No problem! Thanks to LangChain’s modular design, you can swap providers with just a few lines of code—as shown below, with just two small changes, LangChain allows us to swap between different LLMs and embedding models effortlessly. Let’s see it in action.

```python
from langchain.llms import GooglePalm
from langchain.chains import RetrievalQA
from langchain.vectorstores import FAISS
from langchain.embeddings import HuggingFaceEmbeddings
from langchain.document_loaders import TextLoader

# Load and process documents
loader = TextLoader("data/sample.txt")  
docs = loader.load()

# Convert documents into vector embeddings (Changed: Using Hugging Face's BGE model)
hf_embeddings = HuggingFaceEmbeddings(model_name="BAAI/bge-large-en")
vectorstore = FAISS.from_documents(docs, hf_embeddings)

# Create a retrieval-augmented QA system (Changed: Using Google Gemini Pro instead of GPT-4)
llm = GooglePalm(model_name="gemini-pro")
qa_chain = RetrievalQA.from_chain_type(llm=llm, retriever=vectorstore.as_retriever())

# Ask a question
query = "What is LangChain?"
answer = qa_chain.run(query)
print(answer)
```

Just by changing two lines of code, you were able to switch models and embeddings, without worrying about the backend pipeline and other services.
This showcases why LangChain is a game-changer—instead of being stuck with a single AI provider, you can seamlessly switch between OpenAI, Google, Anthropic, Hugging Face, or even local models with minimal changes!

## 5. LangChain alternatives

Although LangChain is extremely popular there are various other players in the market as well, Several alternatives to LangChain exist, each catering to different needs. LlamaIndex (formerly GPT Index) excels in retrieval-augmented generation (RAG) by enabling structured data retrieval. Haystack by Deepset is a strong choice for search and question-answering applications. Guidance provides fine-grained control over prompt execution, making it ideal for structured text generation. AutoGPT and BabyAGI specialise in autonomous AI agents for multi-step task automation. PromptFlow by Azure is suited for enterprises needing scalable AI workflows. CrewAI enables multiple AI agents to collaborate on complex tasks. For developers seeking flexibility, MLflow and Hugging Face Transformers allow custom LLM pipelines without predefined orchestration frameworks. The best alternative depends on specific requirements, such as retrieval, automation, or enterprise integration.

## TL;DR: Key Takeaways

- Before LangChain, building AI applications required **complex manual orchestration** of multiple components.  
- **Semantic search** helps retrieve only relevant text instead of feeding entire documents to an LLM.  
- **LangChain simplifies integration**, making it **plug-and-play** for AI pipelines with minimal code changes.  
- It supports **multi-LLM compatibility, memory management, RAG, and external tool integrations**.  
- **Alternatives like LlamaIndex & Haystack** also provide solutions for specific AI use cases.  

## Special thanks to Nitish Singh

This article is heavily inspired by Nitish Singh’s LangChain Introduction video[^7] from CampusX. His ability to break down complex concepts into digestible explanations made it much easier for me to understand LangChain and its real-world applications.

The original content was in Hindi, but I wanted to cater this knowledge to a global audience so that more people irrespective of language barriers can benefit from the incredible insights he shared. By structuring this article in English, my goal was to make it accessible to a wider community of AI and machine learning enthusiasts who are eager to explore LangChain.

I sincerely thank Nitish Singh and the CampusX team for their exceptional educational content, which has helped countless learners, including myself, dive deep into LangChain and its capabilities. If you're comfortable with Hindi and want a more in-depth, hands-on introduction to LangChain, I highly recommend checking out Nitish Singh's CampusX video it's a fantastic resource!
🙏 A big thank you to Nitish Sir and CampusX for their invaluable contributions to the AI community!

🚀 **_Exciting News: This is just the first article in a series where I’ll continue breaking down more LangChain concepts! Stay tuned for upcoming deep dives, hands-on implementations, and advanced techniques!_**

## Thank you for reading

I truly appreciate you taking the time to read this article! 🎯 I hope it provided **valuable insights** into LangChain and how it simplifies working with LLMs.  

If you found this helpful, connect with me on [LinkedIn](https://www.linkedin.com/in/kameshkotwani) to discuss more LLM-powered innovations! What are your thoughts on LangChain—have you used it in a project yet?

Let’s keep exploring and building amazing AI applications together! 💡🔥  

## References

[^1]:<https://www.langchain.com/langchain>
[^2]:<https://platform.openai.com/docs/guides/embeddings>
[^3]:<https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html>
[^4]:<https://www.datacamp.com/blog/the-top-5-vector-databases>
[^5]:<https://arxiv.org/abs/1706.03762>
[^6]:<https://ollama.com/library/deepseek-r1:671b>
[^7]:<https://www.youtube.com/watch?v=nlz9j-r0U9U>