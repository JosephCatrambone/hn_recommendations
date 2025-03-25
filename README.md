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

FastAPI or Flask: probably FastAPI so it's easier to define models and we can get the OpenAPI.json to make quick/easy frontend bits.
Basic recommender system for backend.
Easy: Don't train a model; dot product between input text and each article. Fetch API at time-of-use. (No DB here.)
Medium: Don't train a model; prefetch and store vectors with pre-made embedding model.
Advanced: Train a quick mapping model between the person embedding and the story embedding.  

Steps:
- Get cozy with the HN API in a notebook.  Pull and store 500 articles in a DB.  We can use SQLite for ease of distribution but this should be abstracted out so we can swap it for Postgres.
- Checkpoint: can we do basic keyword matching?
- Migrate database to add embeddings.
- Checkpoint: can we do ballpark embedding matching?  How well does the user embedding map to articles?
- Perform actual sorting and ranking on the DB side -- if dot-product between all the top 500 is too slow, we should do a prefilter with BM25 and then a smarter dot afterwards.
