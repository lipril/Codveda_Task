# Yahoo Finance Screener Scraper 📈
### Codveda Technologies - Data Science Internship (Level 1, Task 1)

![Python](https://img.shields.io/badge/Python-3.13-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-2.0+-150458.svg)
![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-4.12+-green.svg)
![curl_cffi](https://img.shields.io/badge/curl__cffi-0.16+-orange.svg)

## 📖 Project Overview
During my 1-month internship at **Codveda Technologies**, I was tasked with building a robust web scraping pipeline to collect financial data. The objective was to identify a target website, inspect its structure, handle dynamic content and pagination, and store the scraped data in a structured format (CSV).

I chose **Yahoo Finance** as the target, specifically the "Most Actives" screener. Yahoo Finance is notoriously difficult to scrape due to its sophisticated anti-bot protections, dynamic JavaScript rendering, and strict API authentication. This project demonstrates my ability to reverse-engineer web applications, manage session authentication, and build resilient data collection pipelines.

## 🚀 Key Achievements & Technical Highlights
*Why this project stands out from standard scraping assignments:*

*   **Bypassed Advanced Anti-Bot Protection:** Instead of using standard `requests` (which fails against Yahoo's TLS fingerprinting), I implemented `curl_cffi` to impersonate a real Chrome 120 browser at the network level.
*   **Reverse-Engineered API Authentication:** Successfully extracted Yahoo's dynamic `crumb` token and managed session cookies to authenticate with their internal JSON API.
*   **Handled Dynamic Content:** Bypassed JavaScript rendering entirely by targeting the underlying API endpoint (`query1.finance.yahoo.com`), resulting in a 10x faster and more reliable scrape.
*   **Robust Error Handling & Fallbacks:** Built logic to detect API schema changes (e.g., Yahoo occasionally renames the `records` key to `quotes`) and automatically adapt to prevent data loss.
*   **Pagination Management:** Implemented a paginated loop to extract all 382+ available records across multiple API calls with respectful rate-limiting delays.

## 🛠️ Tech Stack & Tools
*   **Language:** Python 3.13
*   **HTTP Client:** `curl_cffi` (Advanced TLS impersonation)
*   **HTML/JSON Parsing:** `BeautifulSoup4`, `json`
*   **Data Manipulation:** `pandas`, `numpy`
*   **Environment:** Jupyter Notebook / Anaconda

## ⚙️ Project Architecture & Workflow

The pipeline is divided into four distinct phases:

### 1. Session Initialization & Authentication
Yahoo Finance requires a valid `crumb` token linked to a session cookie to access its data. 
*   The script initializes a session using `curl_cffi` impersonating Chrome 120.
*   It visits `finance.yahoo.com` to acquire tracking cookies.
*   It calls the `/v1/test/getcrumb` endpoint to retrieve the dynamic authentication token.

### 2. Data Extraction (API Targeting)
Instead of parsing messy HTML, the script queries the internal JSON endpoint:
`https://query1.finance.yahoo.com/v1/finance/screener/predefined/saved`
*   Passes the `scrIds="most_actives"` parameter.
*   Implements a fallback mechanism: if the standard `records` key is missing, it dynamically searches for `quotes`, `rows`, or `data` keys.

### 3. Pagination Loop
The script paginates through the dataset by incrementing the `offset` parameter (e.g., 0, 25, 50...) until it reaches the total available records. A `time.sleep(1)` is applied between requests to respect Yahoo's servers and avoid rate-limiting.

### 4. Data Wrangling & Export
The raw nested JSON is flattened using `pandas.json_normalize()`. 
*   Handles nested dictionaries like `{'raw': 123.45, 'fmt': '123.45'}`.
*   Exports two distinct datasets for different use cases (see below).

## 🔍 Critical Analysis

While the scraper successfully retrieves and structures the data, a critical evaluation reveals both strengths and areas for improvement:

**Strengths:**
- **Robustness:** The use of `curl_cffi` and the fallback logic for API schema changes makes the script significantly more resilient than standard scrapers.
- **Data Quality:** The output is highly structured, with both a full dataset (for deep analysis) and a curated dataset (for quick insights).
- **Efficiency:** By targeting the API rather than rendering the full page with Selenium/Playwright, the script is fast and lightweight.

**Limitations:**
- **Maintenance Overhead:** Yahoo Finance can change its API endpoints, `crumb` logic, or response schema at any time. This script requires periodic manual updates to remain functional.
- **Synchronous Execution:** The script fetches pages sequentially. For scraping thousands of records, implementing asynchronous requests (`asyncio` + `aiohttp`) or multi-threading would significantly improve speed.
- **Data Freshness:** The script captures a snapshot in time. It does not handle real-time streaming data or historical time-series data.

**Ethical Considerations:**
- Web scraping must be conducted responsibly. This script includes a `time.sleep(1)` delay between requests to respect Yahoo Finance's server load and avoid rate-limiting.
- Users must ensure their usage complies with Yahoo Finance's Terms of Service and `robots.txt` guidelines.

---

## 🏁 Conclusion

Completing this task at Codveda Technologies was a pivotal experience that bridged the gap between academic theory and real-world data engineering. It challenged me to think like an engineer—solving authentication puzzles, handling unstructured data, and writing resilient code. 

This project demonstrates not only my technical proficiency with Python and Pandas but also my ability to research, adapt, and deliver a production-ready solution to complex data collection problems. I look forward to applying these skills to larger, more complex datasets in future data science and analytics projects.

---
## 🤝 Contributing

Contributions, issues, and feature requests are welcome!  
Feel free to check 

---

## 📄 License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

---

## 👥 Author

**Your Name**  
- GitHub: [@lipril](https://github.com/lipril)  
- LinkedIn: [LinkedIn](https://www.linkedin.com/in/liprilomar/)

---

## 🙏 Acknowledgments

- Dataset source: Yahoo Finance

---

**⭐ If you find this project useful, please consider giving it a star!**
## 📂 Repository Structure
```text
├── Data Collection Task 1 L1.ipynb   # Main Jupyter Notebook containing the scraper
├── yahoo_screener_full.csv           # Raw, flattened output (400 rows, 168 columns)
├── yahoo_screener_curated.csv        # Cleaned, minimal output (400 rows, 3 columns)
└── README.md                         # Project documentation

