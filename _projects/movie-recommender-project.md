---
layout: single
title: " 🎬 just another movie recommender system 🎬"
project_title: " 🎬 movie recommender 🎬"
date: 2023-03-01
description: "a streamlit application which recommendes movies using imdb dataset."

categories: [Machine Learning, Reccomendation System]
tags: [pandas,python,streamlit,git,github,streamlit cloud,nlp,tf-idf vectorisation, cosine similarity, AI, movies dataset]
sidebar:
  - title: "project resources"
    text: |
      - [deployed app](https://kameshkotwani-movie-recommender-app-2ef4kr.streamlit.app/)
      - [source code](https://github.com/kameshkotwani/movie-recommender)
      - [kaggle - dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata)

author_profile: true
classes: wide
related: true
read_time: true
header:
    teaser: assets/images/movie-recommender-header.png
---
A streamlit application which recommendes movies using imdb dataset.

## [see it in action](https://kameshkotwani-movie-recommender-app-2ef4kr.streamlit.app/)

![Movie Recommender Demo]({{ site.url }}{{ site.baseurl }}/assets/gifs/movie-recommender.gif)

## the problem: too many choices

Ever found yourself endlessly scrolling through movie lists, struggling to pick the perfect one? We've all been there. Platforms like **netflix, amazon prime, and disney+** seem to know exactly what we’d like to watch next—but how do they do it? 🤔  

Curious about the magic behind these recommendation systems, I decided to **build my own movie recommender system**! 🎬 Not just to solve my own indecisiveness but also to deep dive into how machine learning powers personalized recommendations.

## the approach: content-based filtering 

When it comes to recommendation systems, there are multiple approaches. Many platforms, like Netflix and Spotify, use **Collaborative Filtering**, which relies on user interactions—what users watch, rate, or interact with. However, since I wanted to focus purely on understanding **how movies are related to each other** based on their descriptions and genres, I implemented a **Content-Based Filtering** system.  

## but how does content-based filtering work?

Content-Based Filtering recommends items (movies, in this case) **based on their features** rather than user behavior. The idea is simple:  

- If you like a movie, chances are you’ll enjoy another movie **with similar content** (genre, description, cast, etc.).  
- Instead of relying on user preferences or ratings, the system analyzes the actual content of the movie and finds others that are closely related.  

## **extracting meaning from movie descriptions: TF-IDF vectorization**  

Since the core idea is to recommend movies based on their plot summaries, I used **TF-IDF (Term Frequency-Inverse Document Frequency) Vectorization**.  

**why TF-IDF?**  

Movie descriptions are just blocks of text, and machine learning models need numerical input. TF-IDF converts text into meaningful numerical representations by:  

- **Emphasizing important words** that appear frequently in a movie’s description.  
- **Reducing the weight of common words** like “the” or “and” that appear in almost every description.  

This way, we can **capture the essence of a movie's storyline** and compare it with others.  

## **measuring similarity: cosine similarity**  

Now that each movie’s description is transformed into a numerical vector, we need a way to **measure how similar two movies are**. This is where **Cosine Similarity** comes in.  

**why cosine similarity?**  
Cosine Similarity measures the **angle between two vectors** in a multi-dimensional space. If two movies have similar descriptions, their vectors will be close to each other, and the cosine similarity score will be **closer to 1** (meaning they are very similar).  

**mathematically, cosine similarity is calculated as:**  

$$
\text{cosine similarity} = \frac{A \cdot B}{||A|| ||B||}
$$

where:  

- \( A \) and \( B \) are the TF-IDF vectors of two movies.  
- The **dot product** in the numerator measures the similarity between the vectors.  
- The **denominator normalizes the values**, preventing bias from longer descriptions.  

### **final flow of the recommendation system**  

<div >
    <p align="center" style="border: 1px solid #000">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/user-flow-movie-recommender.jpeg" alt="recommender flow" />
    </p>
</div>

🚀 **Result?**  
Instead of random or generic suggestions, the model **intelligently picks movies that have a similar storyline, genre, and themes**, just like how real-world recommendation engines work! 🎬🔥  

This approach gave me a **hands-on understanding of how platforms like Netflix generate recommendations**, and I’m excited to improve it further by experimenting with hybrid models in the future! 🚀

