```markdown
# AI Medical Chatbot - Interviewer

An advanced AI-powered medical chatbot designed to conduct structured clinical interviews and generate detailed psychological reports. Built with Retrieval-Augmented Generation (RAG) using a FAISS vector database, this tool supports multilingual interactions (including Hindi) and offers flexible interview lengths (10–25 questions). It includes two virtual interviewers—Sarah (compassionate) and Aaron (direct)—and can process uploaded patient documents for report generation.

## Directory Structure

```
8-Interviewer/
├── hf/                       # Core application code
│   ├── ai_config.py          # OpenAI API configuration
│   ├── app.py               # Gradio UI and main logic
│   ├── knowledge_retrieval.py # FAISS-based knowledge retrieval
│   ├── prompt_instructions.py # Interviewer prompts and report templates
│   ├── settings.py          # Interview flow and utilities
│   ├── appendix/            # Documentation and visuals
│   │   ├── description.txt  # Description tab content
│   │   └── diagram.png      # System architecture diagram
│   └── requirements.txt     # Python dependencies
├── knowledge/                # Vector database files
│   ├── embeddings.npy       # Embeddings for dialogues
│   └── faiss_index_all_documents/
│       ├── index.faiss      # FAISS index
│       └── index.pkl        # FAISS metadata
├── make the vectordatabase for the llm/  # Vector database creation
│   ├── 2-Data.ipynb         # Data processing notebook
│   ├── 3-Compression.ipynb  # Data compression notebook
│   ├── dialogues_embededd.pkl  # Embedded dialogue data
│   ├── fiss.py             # FAISS index creation script
│   ├── dialogues_dataset_card.md  # Dataset description
│   ├── dialogues_metadata.yaml    # Dataset metadata
│   ├── Readme.md           # Vector DB creation guide
│   └── tools/
│       ├── Notes.txt       # Clinical notes
│       └── timer.py        # Timing utility
└── README.md               # This file
```

## Features

- **Interactive Interviews**: Conducts interviews with four fixed questions ("What is your name?", "What is your age?", "Where do you live?", "What is your current occupation?") followed by dynamic, tailored follow-ups.
- **Customizable Settings**: Choose between 10–25 questions, select interviewers (Sarah or Aaron), enable audio output, and pick from multiple languages (English, Hindi, Spanish, French, German, Italian).
- **Multilingual Support**: Questions and reports are translated to the selected language; user input is translated to English for processing.
- **Report Generation**: Produces detailed clinical reports with psychological assessments (e.g., Big Five Traits, Personality Disorders) after interviews or from uploaded documents (TXT, PDF, DOCX).
- **Knowledge Base**: Integrates a FAISS vector database for RAG, built from medical dialogue data.

## Prerequisites

- Python 3.8+
- Libraries: Listed in `hf/requirements.txt` (e.g., `gradio`, `langchain-community`, `langchain-openai`, `faiss-cpu`, `openai`, `PyPDF2`, `python-dotenv`)
- OpenAI API key (stored in `.env`)

## Setup

1. **Clone the Repository**
   ```bash
   git clone https://github.com/Kaustubh-Rathi/ai-medical-chatbot-master.git
   cd ai-medical-chatbot-master/8-Interviewer
   ```

2. **Install Dependencies**
   ```bash
   pip install -r hf/requirements.txt
   ```

3. **Set API Key**
   Create a `.env` file in the root directory:
   ```
   OPENAI_API_KEY=your-openai-api-key
   ```

4. **Prepare the Vector Database** (if not already present)
   - Navigate to `make the vectordatabase for the llm/`.
   - Follow the instructions in its `Readme.md`:
     1. Run `2-Data.ipynb` to process dialogue data.
     2. Run `3-Compression.ipynb` to compress data.
     3. Run `fiss.py` to create the FAISS index (`knowledge/` outputs).

## Usage

1. **Run the Application**
   ```bash
   python hf/app.py
   ```
   - Opens a Gradio interface in your browser.

2. **Interview Tab**
   - Click "Start Interview" to begin.
   - Select language, interviewer, and question count (10–25) in the settings.
   - Respond via text or voice (if audio is enabled).
   - Download the report after completion or end early with "End Interview".

3. **Upload Document Tab**
   - Upload a patient document (TXT, PDF, DOCX).
   - Select a language and click "Generate Report".
   - Download the resulting clinical report.

4. **Description Tab**
   - View usage instructions and the system architecture diagram.

## System Architecture

The application follows a modular design:
- **Gradio UI**: Handles user interaction (interview, document upload).
- **OpenAI LLM**: Powers question generation, translations, and report writing.
- **FAISS Vector DB**: Provides RAG context from medical dialogues.
- **Audio Pipeline**: Converts text to speech in the selected language.

See `hf/appendix/diagram.png` in the Description tab for a visual representation.

## Data Sources

- Vector database built from dialogues sourced from [healthcaremagic.com](https://healthcaremagic.com) and [icliniq.com](https://icliniq.com).
- Processed in `make the vectordatabase for the llm/`.

## Notes

- Ensure the `knowledge/` folder contains the FAISS index (`index.faiss`, `index.pkl`) and embeddings (`embeddings.npy`) before running the app.
- Audio output requires a working OpenAI TTS setup and may vary in quality across languages.

## GitHub Upload

1. **`.gitignore`** (recommended):
   ```
   *.csv
   *.parquet
   *.pkl
   knowledge/
   .env
   __pycache__/
   ```

2. **Push to GitHub**:
   ```bash
   git add .
   git commit -m "Initial commit of AI Medical Chatbot - Interviewer"
   git push origin master
   ```

## Contributing

Feel free to fork this repository, submit issues, or propose enhancements via pull requests. Focus areas include improving translation accuracy, expanding language support, or optimizing the vector database.

## License

This project is licensed under the MIT License—see [LICENSE](LICENSE) for details (add if applicable).

---
```


