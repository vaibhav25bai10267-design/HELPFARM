# HELPFARM
# SIH PitchDeck AI

A small, local web app that turns a Smart India Hackathon (SIH) problem statement into a concise, editable PowerPoint using the supplied NMIET SIH 2026 template. It uses Ollama for locally hosted language models; TinyLlama is the default model for this project.

## Features

- Generates exactly six presentation slides: Title Page, Proposed Solution, Technical Approach, Feasibility and Viability, Impact and Benefits, and Research and References.
- Fills the first six slides of the supplied template and omits its seventh, submission-instructions slide.
- Draws an editable four-step flow diagram with PowerPoint shapes and connectors on the Technical Approach slide.
- Accepts the problem statement, problem ID, project title, theme, category, team ID, team name, and optional context.
- Saves generated files in `outputs/` and offers the PowerPoint for download.
- Exports a PDF when LibreOffice is installed. Otherwise, download the PowerPoint and export it to PDF from PowerPoint.
- Runs without sign-in, a database, a cloud AI key, or sending prompts to a hosted AI service. Ollama must be running locally.

## Requirements

- Windows
- Python 3
- Ollama
- A downloaded Ollama model (TinyLlama is the default)
- `python-pptx` (install from `requirements.txt` if the Python selected by `start.bat` does not already have it)
- LibreOffice is optional and needed only for automatic PDF export

## Setup and run

1. Install [Ollama](https://ollama.com/) and start it.
2. Download TinyLlama from a terminal:

   ```powershell
   ollama pull tinyllama
   ```

   You can use another model already installed in Ollama by selecting it in the app.

3. If needed, install the Python dependency from the project folder:

   ```powershell
   py -3 -m pip install -r requirements.txt
   ```

4. Double-click `start.bat`. Keep the terminal window open while using the app. The script checks for a compatible Python runtime and starts the local server on port `8766`.
5. Open [http://localhost:8766](http://localhost:8766) in your browser.
6. Enter the problem statement and team information, select an available Ollama model, and choose **Generate my 6-slide deck**.
7. Download the `.pptx` from the success message. Generated files are also saved in `outputs/`.

## Run from a terminal

From the project folder, start the server with Python:

```powershell
py -3 server.py
```

Then open [http://localhost:8766](http://localhost:8766). If the `py` launcher is unavailable, run `python server.py` instead.

## Template slide mapping

| Slide | Section |
| --- | --- |
| 1 | Title Page and team metadata |
| 2 | Proposed Solution |
| 3 | Technical Approach and editable solution flow |
| 4 | Feasibility and Viability |
| 5 | Impact and Benefits |
| 6 | Research and References |

The template asks for a maximum of six slides including the title page. Its final slide contains instructions, so it is not included in generated submissions.

## Notes and troubleshooting

- **No models appear:** Start Ollama, run `ollama pull tinyllama`, then refresh the app page.
- **Ollama connection error:** Confirm Ollama is running and available at `http://localhost:11434`.
- **Python dependency error:** Run `py -3 -m pip install -r requirements.txt`, then start `start.bat` again.
- **The success message says a starter draft was used:** The selected local model returned incomplete structured content. Review the generated slides and edit them in PowerPoint before submitting.
- **No PDF link appears:** Install LibreOffice for automatic conversion, or export the downloaded PowerPoint to PDF using PowerPoint.

Generated AI content can contain mistakes. Verify technical claims, references, and project details before presenting or submitting the deck.

## Project files

- `server.py` — local web server, Ollama integration, and PowerPoint/PDF generation
- `index.html` — browser interface
- `NMIET_SIH_2026_PPT_Template.pptx` — fixed presentation template
- `requirements.txt` — Python package dependency
- `start.bat` — Windows launcher
- `outputs/` — generated presentations
