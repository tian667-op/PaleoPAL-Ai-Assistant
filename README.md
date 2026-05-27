# PaleoPAL-Ai-Assistant
PaleoPAL Ai assistant program powered by LLM Anthropic Claude Ai
## Features

- **AI Research Q&A** — Ask any paleoclimatology question and get scientifically rigorous answers powered by Claude AI, with full multi-turn conversation support
- **Real Proxy Data** — Fetches live data directly from three major public paleoclimate databases — no static files, always up to date
- **Proxy Data Analysis** — Statistical analysis tailored to each proxy type including time series smoothing, anomaly detection, linear trend testing, and Lomb-Scargle spectral analysis
- **AI Interpretation** — Automatically generates a scientific interpretation of your analysis results using Claude AI
- **Multi-Proxy Comparison** — Correlates and compares two proxy records over their overlapping time period with AI-assisted interpretation
- **Interactive Widgets** — Built-in Jupyter widgets for a clean point-and-click interface


## Supported Proxy Types

| Proxy | Variables | Data Source |
|---|---|---|
| Ice cores | δ¹⁸O, δD | NOAA Paleoclimatology |
| Tree rings | Ring width index | NOAA ITRDB |
| Sediment / pollen | Pollen %, assemblages | Neotoma, PANGAEA |


## Data Sources

PaleoPAL connects to live public databases continuously updated by the global research community:

- **NOAA Paleoclimatology** — ncei.noaa.gov/products/paleoclimatology
- **Neotoma Paleoecology Database** — neotomadb.org
- **PANGAEA** — pangaea.de

Every time you run the notebook you get the most current available data from each source.


## Requirements

- Python 3.10+
- Jupyter Notebook 7.0+
- Anthropic API key — get yours at console.anthropic.com

## Installation

### 1. Clone this repository
```
git clone https://github.com/tian667-op/PaleoPAL-Research-Assistant.git
cd PaleoPAL-Research-Assistant
```

### 2. Install dependencies
```
pip install -r requirements.txt
```

### 3. Set up your credentials

Mac / Linux / Git Bash:
```
cp .env.example .env
```

Windows Command Prompt:
```
copy .env.example .env
```

Then open the `.env` file and replace the placeholder with your Anthropic API key.

### 4. Launch Jupyter Notebook
```
jupyter notebook
```

Open `PaleoPAL.ipynb` and run all cells from top to bottom.

---

## Configuration

| Variable | Description | Where to get it |
|---|---|---|
| `ANTHROPIC_API_KEY` | Your Claude AI API key | console.anthropic.com |

---

## Usage

### Research Q&A
```python
ask_paleopal("What can δ18O values from ice cores tell us about past temperatures?")
ask_paleopal("How do I calibrate radiocarbon dates from a lake sediment core?")
ask_paleopal("What spectral analysis method is best for unevenly spaced proxy data?")
```

### Fetch Real Data
```python
# Search NOAA for ice core studies
studies = search_noaa("ice_core", keyword="GISP2", max_results=5)

# Fetch the GISP2 Greenland Ice Core (110,000 yr record)
dataset = fetch_noaa("2475", proxy_type="ice_core")

# Search Neotoma for pollen records
sites = search_neotoma(taxon="Quercus", dataset_type="pollen", limit=5)

# Fetch a pollen dataset
dataset = fetch_neotoma(dataset_id=4116, taxon="Quercus")

# Search and fetch from PANGAEA
results = search_pangaea("Holocene lake sediment pollen", max_results=5)
dataset = fetch_pangaea("728846", proxy_type="sediment")
```

### Run Full Analysis Pipeline
```python
# Load → Analyze → Plot → Interpret
dataset = fetch_noaa("2475", proxy_type="ice_core")
results = analyze_proxy(dataset)
plot_proxy(results)
plot_spectral(results)
interpret_proxy(results)
```

### Compare Two Proxy Records
```python
compare_proxies(
    "ice_core", "sediment",
    label_a="Ice Core δ¹⁸O",
    label_b="Sediment Pollen %"
)
```

---

## Function Reference

| Function | Description |
|---|---|
| `ask_paleopal(question)` | Ask any paleoclimate research question |
| `reset_conversation()` | Clear conversation history |
| `search_noaa(proxy_type, keyword)` | Search NOAA Paleoclimatology |
| `fetch_noaa(study_id)` | Fetch a NOAA study by ID |
| `search_neotoma(taxon)` | Search Neotoma by pollen taxon |
| `fetch_neotoma(dataset_id, taxon)` | Fetch a Neotoma pollen dataset |
| `search_pangaea(keyword)` | Search PANGAEA by keyword |
| `fetch_pangaea(pangaea_id)` | Fetch a PANGAEA dataset by ID |
| `load_proxy_data(source)` | Load a CSV file or sample dataset |
| `analyze_proxy(dataset)` | Run full statistical analysis |
| `plot_proxy(results)` | Generate time series analysis figure |
| `plot_spectral(results)` | Generate Lomb-Scargle periodogram |
| `interpret_proxy(results)` | AI scientific interpretation |
| `compare_proxies(a, b)` | Compare and correlate two records |


## Dependencies

anthropic
pandas
numpy
matplotlib
scipy
ipywidgets
requests

Install all at once:

pip install -r requirements.txt



## Author

Full Name: Qi Tian
LinkedIn: linkedin.com/in/tian667


## License

MIT License — free to use and modify with attribution.
