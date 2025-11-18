# ESG-NLP-Scorer
Simple application with front end which pulls news from company/firm and assigns esg ratings based on related articles

taken ispo from this site -- https://www.lseg.com/en/data-analytics/sustainable-finance/esg-scores

Project Files

**app.py -** builds the Flask web UI, wiring form submissions to SEC scraping and ESG scoring; it calls get_filing_urls/get_real_10k_document_url from src/sec_fetcher.py and filter_esg_sentences from src/scoring.py, then renders templates/index.html with any results.

**templates/index.html -** Jinja2 template that renders the ticker form, error messages, the list of scored ESG sentences, and a simple theme-frequency summary fed in from app.py.

**src/main.py -** the CLI workflow: it loops through tickers, fetches 10-Ks via get_filing_urls/get_real_10k_document_url, scores sentences with filter_esg_sentences, prints a console summary, and persists results to CSV/JSON files.

**src/sec_fetcher.py -** contains the SEC-facing helpers: a hard-coded CIK_MAP, get_filing_urls to collect recent 10-K filing index URLs, and get_real_10k_document_url to drill into the actual 10-K document. It also embeds a copy of the scoring helpers at the bottom (lines 126–193); those duplicates are unused when importing src.scoring.

**src/scoring.py -** defines the ESG keyword dictionaries, the sentence scoring routine, and filter_esg_sentences, which tokenizes the 10-K text with NLTK, scores each sentence, logs debug output, and returns the high-scoring ones used by both the CLI and Flask app.

**src/__init__.py -** is an empty marker so src can be imported as a package.

**esg_disclosures.csv -** at the repo root is the append-only log written by the CLI script for every scored sentence.

**data/*.json** and **data/esg_disclosures.csv** are sample artifacts produced by the CLI run—each JSON mirrors the structure from save_to_json in src/main.py.

**app/** is currently empty—likely a placeholder for future assets.
**venv/** is a local Python virtual environment (tools and dependencies).
