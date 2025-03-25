This is a repository for a HackerNews Reranking and Search Application

```
Build an API that given user submitted bio, returns top 500 stories from Hacker News front page (use their API for this), ranked in the order of relevancy to user's interests.

Example input:
I am a theoretical biologist, interested in disease ecology. My tools are R, clojure , compartmentalism disease modeling, and statistical GAM models, using a variety of data layers (geophysical, reconstructions, climate, biodiversity, land use). Besides that I am interested in tech applied to the a subset of the current problems of the world (agriculture / biodiversity / conservation / forecasting), development of third world countries and AI, large language models.

Output:
Top 500 items from Hacker News, ranked in the order of relevance to the user.

The solution should optimize for development time - what is the simplest/quickest way to do this that you can think of? Spend no more than 4 hours on this.
Deliverables

    GitHub Repo
    Link to a live demo containing a text area for the input and a button to submit. The results will be shown below.
    Explain your thought process and decisions you made during creation of the solution.

Main task - Query reformulation ML model

Build an API to a machine learning model that given an input query can generate one or more adequate search engine queries to obtain requested information.

Your API should have maximum 100ms latency on a consumer grade CPU.

Examples of good API outputs for given inputs:

    In what year was the winner of the 44th edition of the Miss World competition born?
    44th Miss World competition winner birth year

    Who lived longer, Nikola Tesla or Milutin Milankovic?
    Nikola Tesla lifespan
    Milutin Milankovic lifespan

    Author David Chanoff has collaborated with a U.S. Navy admiral who served as the ambassador to the United Kingdom under which President?
    David Chanoff U.S. Navy admiral collaboration
    U.S. Navy admiral ambassador to United Kingdom
    U.S. President during U.S. Navy admiral's ambassadorship

    Create a table for top noise cancelling headphones that are not expensive
    top noise cancelling headphones under $100
    top noise cancelling headphones $100 - $200
    best budget noise cancelling headphones
    noise cancelling headphones reviews

    what are some ways to do fast query reformulation
    fast query reformulation techniques
    query reformulation algorithms
    query expansion methods
    query rewriting approaches
    query refinement strategies

Deliverables

    GitHub Repo
    Link to a live demo containing an input field. The results will be shown below.
    Explain your thought process and decisions you made during creation of the solution.
```

Game Plan - Day 1

We need a UI that's reasonable and straightforward.  I don't want to split off a frontend and backend component because it makes iterating on the project slower, makes it harder to ship, and we really don't need the things that client-side rendering will offer to us.  Something like Gradio seems like a good option.
The backend seems like a basic recommender system.  If I don't want to train a model (in the four hours I have to complete), then I could do something simple like use a pre-made embedding model and a dot-product between the user vector and the articles.

Steps:
- Pull 500 articles from HN.
- Make a UI with gradio that can share the top 500 in some order.  Better to get the data showing early.
- Write the headlines and links to a database (postgres or sqlite with pgvec?) with embeddings.
- Perform actual sorting -- if dot-product between all the top 500 is too slow, we should do a prefilter with BV25 and then a smarter dot afterwards.
