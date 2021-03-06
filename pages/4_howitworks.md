---
layout: page
title: How It Works
published: true
---

The following is an overview of the workflow of our tool, which describes how our tool works, after being given the text of an article as input:

- We pass the text to Stanford CoreNLP, which has models that do common natural language processing (NLP) tasks. Specifically, CoreNLP does parsing, part-of-speech tagging, named entity recognition, coreference resolution and quote detection. It annotates our text with the outputs of these various NLP tasks, and our tool then works with these annotations.
- Now that we have the annotations, our first step is to identify the set of all mentions of people in the article. We do this by simply scanning over the text word-by-word, and using CoreNLP’s named entity recognition output to tell if the current word is a mention of a person.
- After identifying the set of all mentions of people in the article, we add contextual information for each mention: what pronouns/nouns each mention is coreferent with (two words in a text are coreferent if they refer to the same real-world entity); what honorific, if any, is there before the mention; and so on. Using all this contextual information, we attempt to tag each mention with a gender. For example, if the mention is preceded by Mr., we tag it as male; if the mention is coreferent with ‘she’, we tag it as female.
- Next, we begin a crucial task: that of merging mentions which refer to the same individual, so that at the end, we have a list of unique individuals that are mentioned in the article. To do this, we use the contextual information around each mention, as well as some heuristics, which we came up with based on insights from the error analysis we performed.
- To identify who has a voice in the article, we use CoreNLP’s quote detection output, along with the information we have built up about which person is mentioned where in the article, to attribute quotes to the different people mentioned in the article. We also use the parse of the sentence to see if the person is the subject (in the grammatical sense) of a noun that is associated with speaking, like say, tell, or speak.
