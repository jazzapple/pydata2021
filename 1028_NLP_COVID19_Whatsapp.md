# Highly Scalable NLP to Answer Questions on South Africa's COVID-19 WhatsApp hotline

* HealthConnect for COVID - national WhatsApp information service - government and health orgs
    * Initially menu dependent in response to text inputs
    * Subsequently incorporated Q&A  in natural language - resource challenge for human answering capability
        * Can't be any old chatbot - presence of misinformation, accuracy is critical, explainability is key
    h    * So can't just use off the shelf language model
        * need something quite supervised - most NLP models are not

## Solution
* Solution must centre on a store of FAQs to ensure true content (even if not relevant to what a useres's asking for)        
* Problem reduces to matching user questions to store of FAQs
    * simple - BOWs classifier to FAQ ID
* Challenges
    * no training data. dynamic context
    * FAQ store needs to evolve over time
* Approach
    * Similarity between User Question and Theme of FAQ via embeddings
    * Satisifies dynamic nature of COVID themes
    * For each FAW in the store, assign it relevant tags that need to match a user query. e.g. FAQ: "is it safe to get the vaccine when pregnant?" might have tags ["pregnant", "vaccine", "safe"]
    * Then as new user questions come in, calculate a score for how well it matches the tags in each FAQ
        * from question, use word embeddings that are closests in cosine similarity to FAQ tag to compare and generate score
    * Used Google news pre-trained model - but COVID conversational context in South Africa is unique (vs news headlines in US, Europe) - regional slang, typos e.g. "jab"
* Mis-spellings and typos:
    * spell check / correction packages e.g. `Hunspell`
    * which word should it be? context + embeddings = select most similar to "corrected" words
* Text shorthand / regional phrases
    * use glossary e.g. "jab" >> "vaccine", "covid" >> 0.8* vector(virus) + 0.2*vector(pandemic) linear combination of existing terms in corpus
* Managing inference latency
    * found sklearn check_array and assert_all_finite were expensive, so took out sklearn and used plain old numpy to calculate cosine similarity
    * pre-calculated normalisation component of dot product in cosine similarity so that at runtime only a single call to `np.dot(...)` is required >> reduced latency from 8 calls per second to 100 calls per second

### Results
* 72% successful match rate
* Many questions not covered by FAQ store
    * Real time monitoring of mesage stream (and adaptation of FAQ bank)
    * train new language embeddings
    * model calibration with layer on top of embeddings - latent estimates for each FAQ in store of popularity and accuracy
