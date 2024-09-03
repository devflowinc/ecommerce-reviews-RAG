# ECommerce Customer Reviews RAG

This repo contains an Open Source version of Amazon Rufus, an AI chat UX over customer reviews! We are excited about the potential UX and looking to help make it more ubiquitous. See the live demo at [review-rag.trieve.ai](https://review-rag.trieve.ai/) or watch a [video of it in action here](https://www.loom.com/share/94d432aead0542a398b14cdb636e6b9b?sid=35c4e25b-89e9-4634-b82b-624b46ebf2fe).

## Overview

This is a vanilla JavaScript demo for what could be a configurable component that provides a chatbot interface for customers to ask questions about the product reviews. It includes:

- a generated summary of reviews
- chatbot answers using RAG
- suggested related questions
- a display of the most relevant reviews related to the user's question

<img width="1912" alt="image" src="https://github.com/user-attachments/assets/deecdd5f-394c-4ec3-bdda-16849bfac407">

The initial message is a generated summary of 30 reviews of the product. Here we simply sorted by the `up_vote_count` minus the `down_vote_count`. In the demo, the summary is drawn from a cached value, but you can regenerate it on a different prompt in the userscript or generate the cached values for the three demo products in a sample test script. We used OpenAI's 4o model to generate the summary and you can see the prompt we used in the script. The initial suggested questions are also pre-generated, but each user query will generate *new* suggestions based on the current set of reviews.

The chat response is RAG here, retrieval augmented generation, so for this we conduct a search on the reviews to get the 30 most relevant to the user's question and results are provided as context to the AI model, along with the user's question itself.


## Demo video

On Loom: [ECommerce Customer Reviews RAG Live Demo](https://www.loom.com/share/94d432aead0542a398b14cdb636e6b9b?sid=35c4e25b-89e9-4634-b82b-624b46ebf2fe)

## Running the userscript

This repo has a userscript (`trieve-reviews-integration.user.js`) that you can inject into the product pages with the [TamperMonkey](https://www.tampermonkey.net/) extension.

- If you don't have the TamperMonkey installed, you can get it for Chrome [here](https://chromewebstore.google.com/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo).
- In Chromium-based browsers you will need to set "Developer mode" to 'on' in your overall extension settings.
    - In Chromium this is at: `chrome://extensions/` (top right corner)
- Then you can navigate to one of the supported product pages:
    - [The Annie](https://www.tecovas.com/products/the-annie)
    - [The Doc](https://www.tecovas.com/products/the-doc)
    - [The Jamie](https://www.tecovas.com/products/the-jamie)
- On the first interaction with the interface, a new page will appear saying: "A userscript wants to access a cross-origin resource." You will need to click one of the 'Allow' options.

## Running the Trieve API routes

You can also use the test-trieve-frontend-routes.js node script to explore the routes without the frontend components.

Installing axios and then run `node test-trieve-frontend-routes.js` or (just `yarn add` and `yarn start`)
