# NLP RAG Evaluation Project

This project implements and evaluates a Retrieval-Augmented Generation (RAG) system using various NLP techniques. The system processes documents, generates QA pairs, and evaluates the quality of RAG responses.

## Project Structure
project/ <br>
├── main.ipynb # Main notebook containing all implementation <br>
├── data/ # Directory for storing data <br>
│ └── indexes/ # FAISS indexes <br>
├── output/ # Output directory for results <br>
│ ├── QAs.json # Generated QA pairs <br>
│ ├── Critiques.json # Evaluation results <br>
| ├── rag_final_result.json # Final RAG evaluation results <br>
│ └── Evaluation_Result.json # evaluation results LLm as judge <br> 

## Features

1. **Document Processing**
   - Supports multiple file formats (PDF, TXT, DOCX, CSV, XLSX)
   - Implements chunking with RecursiveCharacterTextSplitter
   - Handles metadata extraction

2. **QA Generation**
   - Generates question-answer pairs from document chunks
   - Uses LLM (Groq) for QA generation
   - Implements quality filtering based on groundedness and relevance

3. **RAG Implementation**
   - Uses FAISS for vector storage
   - Implements OpenAI embeddings
   - Includes context retrieval and answer generation

4. **Evaluation System**
   - Evaluates generated answers against reference answers
   - Provides detailed feedback and scoring
   - Generates comprehensive evaluation reports

## Requirements
  - python
  - langchain
  - openai
  - groq
  - faiss-cpu
  - pandas
  - tqdm
  - transformers

## Usage

1. **Setup Environment**
   ```bash
   pip install -r requirements.txt
   ```

2. **Configure API Keys**
   ```python
   import os
   os.environ["OPENAI_API_KEY"] = "your-api-key"
   ```

3. **Load and Process Documents**
   ```python
   data = load_document('your_document.pdf')
   docs_processed = split_documents(chunk_size=300, knowledge_base=data)
   ```

4. **Generate QA Pairs**
   ```python
   outputs = run_rag_tests(
       eval_dataset=generated_questions,
       llm=call_llm,
       knowledge_index=knowledge_index,
       output_file="output/rag_final_result.json"
   )
   ```

5. **Evaluate Results**
   ```python
   evaluate_answers(
       'output/Evaluation_Result.json',
       Rag_outputs,
       eval_chat_model,
       evaluation_prompt_template
   )
   ```

## Evaluation Metrics

The system evaluates Questions & answers based on:
- Groundedness : how relevante is the question compaired to question (1-5 scale)
- Relevance (1-5 scale)
<br>
The system evaluates Rag Answers based on: <br>
   - a feedback and score between 1 & 5 <br>
   - Answer accuracy compared to reference

## Output Format

The evaluation results are stored in JSON format with the following structure:
  ```json
  {
  "question": "...",
  "true_answer": "...",
  "generated_answer": "...",
  "eval_score": "...",
  "eval_feedback": "..."
  }
  ```
## Contact
<a href = 'ziadabadwy@gmail.com'>ziadabadwy@gmail.com</a>
