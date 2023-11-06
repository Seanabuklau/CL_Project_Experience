# CL_Project_Experience

## Introduction
This project was created as part of the BSc Computing & Law Project Experience assignment. The motivation behind this project was to create a punishment calculator for drugs offences in Singapore as part of the collaboration with Prison Fellowship Singapore. This would solve one of the pain points that the project sponsor was facing, that is knowing the estimated punishment that its beneficiaries were to receive base off their case details or charge sheet. This would expedite the process of rendering better social assistance like counselling and prayer to their beneficiaries. 

*Note that this project is still in beta and is presently being improved along the way.*

## Data
The data used is the Misue of Drugs Act 1973 and case laws taken from eLitigation or LawNet. The data would be used to ground the LLM to prevent hallucinations when estimating the punishments that would be rendered. 

## Methodology
The proposed methodology is to leverage Retrieval Augmented Generation (RAG) coupled with Large Language Models to help with this estimation task. Since LLMs are trained on a vast array of text data, the assumption is that the model is well capable of understandning the query in natural language i.e. case details and provide a rough estimate by referencing the law. 

RAG is used here to improve the performance of LLMS by augmenting them with information from external knowledge sources i.e. law, cases. As LLMs are trained on massive amounts of text data, they can still struggle with tasks that require access to specific facts or information especially this case concerning Singapore's Drugs Laws. RAG addresses this issue by allowing LLMs to retrieve and incorporate relevant information from external sources at generation time.

## Steps
### i. Parse Corpus
The first step is to parse the corpus into the worflow. Here, the tool used will be LangChain's Document Loaders.

### ii. Chunk
Then, the corpus will be chunked into sizes of 5000 characters, dividing the data into smaller, more manageable segments, which makes it easier for the LLM to identify and retrieve the most relevant information for the given task.

### iii. Embed Chunks
Chunks will be embedded with embedding models. Here, 2 models were experimented namely OpenAI's text embedding model -002 and MPNet.

### iv. Load Chunks into Vector Store
The embedded chunks are then loaded into a vector store, in this case Pinecone using LangChain's Pinecone Client function. 

### v. Querying & Prompt Engineering
Now that everything is loaded up, prompts can be carefully engineered to elicit the desired output. LangChain's QA chain provides a convenient pipeline to combine the query inputs, the relevant retrieved data based on the query, and then finally feeding it into the LLM to yield results. 

