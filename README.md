# MULTI-AI-AGENT-RESEARCH-SYSTEM

ResearchMind — Multi-Agent Research System

ResearchMind is an AI-powered research assistant that coordinates multiple specialized agents to turn a topic into a structured research report. It searches the web, reads a relevant source, writes a report, and asks a critic agent to review the result.

The project includes a Streamlit web interface as well as a command-line pipeline.

## Features

- **Search Agent** — uses Tavily to find recent web information and relevant URLs.
- **Reader Agent** — selects a useful result and extracts text from the source page.
- **Writer Chain** — produces a structured report containing an introduction, key findings, conclusion, and sources.
- **Critic Chain** — scores the report and provides strengths and improvement areas.
- **Streamlit interface** — displays pipeline progress, raw research output, the final report, and critic feedback.
- **Markdown export** — downloads the generated report as a `.md` file.

## How the pipeline works

```text
Research topic
      |
      v
Search Agent (Tavily web search)
      |
      v
Reader Agent (URL scraping)
      |
      v
Writer Chain (research report)
      |
      v
Critic Chain (review and score)
```

## Project structure

```text
Multi-agent-research-system/
├── agents.py          # Agent definitions and writer/critic LangChain chains
├── app.py             # Streamlit web application
├── pipeline.py        # Reusable pipeline and command-line entry point
├── tools.py           # Tavily search and webpage scraping tools
├── requirements.txt   # Python dependencies
├── .gitignore         # Ignored local and secret files
└── README.md          # Project documentation
```

## Requirements

- Python 3.10 or newer
- An OpenAI API key
- A Tavily API key
- Internet access for web search and source scraping

## Run the Streamlit application

Start the web interface with:

```bash
streamlit run app.py
```

Streamlit will print a local URL, usually `http://localhost:8501`. Open that URL in a browser, enter a research topic, and select **Run Research Pipeline**.

## Run from the command line

The pipeline can also be run without the Streamlit interface:

```bash
python pipeline.py
```

Enter a topic when prompted. The pipeline prints the search results, scraped content, generated report, and critic feedback to the terminal.

## Configuration

The language model is configured in `agents.py`:

```python
ChatOpenAI(model="gpt-4o-mini", temperature=0)
```

To use a different compatible OpenAI model, update the `model` value. The search tool currently returns up to five Tavily results, while the scraper limits extracted page text to 3,000 characters.

## Notes and limitations

- Generated reports should be checked against the original sources before being used for important decisions.
- Web pages may block automated requests or contain content that is difficult to parse.
- API usage may incur charges from OpenAI and Tavily.
- Search and scraping require an active internet connection.
- The scraper removes scripts, styles, navigation, and footer elements, but it is not a full browser-rendering engine.

## Technology stack

- Python
- Streamlit
- LangChain
- OpenAI
- Tavily
- Beautiful Soup
- Requests
