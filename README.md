# Transcript Intelligence Summarizer

An LLM-powered pipeline that transforms raw business transcripts into structured intelligence briefs; combining summarization, sentiment analysis, theme extraction, and named entity recognition using the Anthropic API.

## What it does

Given a raw business transcript (earnings call, meeting, interview), this tool automatically generates:

- **Executive Summary** — concise overview of key points
- **Key Financial Metrics** — extracted numbers in structured format
- **Sentiment Analysis** — overall tone classification with self-reported confidence level
- **Key Themes** — top topics discussed
- **Named Entities** — people, companies, products, and financial figures mentioned
- **Structured Output** — JSON and PDF export for downstream use

## Why I built this

As part of my AI internship at EY, I wanted to explore how LLMs can automate the manual, time-consuming work of reading and summarizing long business transcripts; a task analysts do regularly in market research and competitive intelligence.

## How it works

Raw transcript
↓
Text cleaning (remove noise)
↓
Chunking with overlap (handle long documents within context limits)
↓
LLM summarization (per chunk via Claude API)
↓
Final synthesis (combine chunks into one report)
↓
Intelligence extraction (sentiment, themes, NER)
↓
Structured output (JSON + PDF)

## Tech Stack

- Python
- Anthropic API (Claude Haiku)
- ReportLab (PDF generation)
- Jupyter Notebook

## Key Engineering Decisions

- **Chunking with overlap**: Transcripts often exceed LLM context limits, so text is split into 2000-word chunks with 100-word overlap to preserve context across boundaries
- **Prompt engineering**: Structured prompts explicitly request specific output formats (numbered lists, tables, categories) for consistent, parseable results
- **JSON output**: Enables downstream integration with dashboards, databases, or other systems
- **PDF export**: Provides a professional, shareable format for business stakeholders
- **Environment variables**: API credentials are stored securely via `.env`, never hardcoded

## Sample Output

See `intelligence_brief.pdf` (best viewed by downloading — GitHub's 
inline preview occasionally fails to render PDFs from this library) for an example output generated from a mock Q3 2024 earnings call transcript.

## Limitations & Future Improvements

- Sentiment confidence is self-reported by the LLM (High/Medium/Low) rather than a calibrated numerical probability score from a trained classifier
- Currently tested on synthetic mock data; next step is integrating real transcripts via SEC EDGAR API
- No automated error handling for failed API calls
- Could add a Streamlit UI for non-technical users
- Potential to add multi-document comparison (tracking sentiment/themes across quarters)

## What I Learned

- Prompt engineering for structured, consistent LLM outputs
- Text chunking strategies for processing long-form documents within context window limits
- Building end-to-end data pipelines from raw text to structured business deliverables
- Secure credential management practices
- The distinction between LLM self-reported confidence and calibrated statistical confidence scores

