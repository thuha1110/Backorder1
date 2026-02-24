# Implementation Plan - Domain Investment Analyzer

The goal is to build a production-ready Streamlit application for analyzing and scoring domain names based on brandability, keyword value, authority, age, TLD, and security.

## Proposed Changes

### [Utils Component]
#### [NEW] [utils.py](file:///d:/Công việc iNET/vide code/domain score/utils.py)
- Domain normalization: Remove `http`, `https`, `www`, convert to lowercase, extract root domain.
- File processing: Handle `.xlsx` and `.csv` uploads using `pandas`.
- Validation: Ensure required columns (`Domain`, `Age`) exist and limit to 2000 records.

### [API Service Component]
#### [NEW] [api_service.py](file:///d:/Công việc iNET/vide code/domain score/api_service.py)
- `get_open_pagerank()`: Integrate with OpenPageRank API.
- `check_google_safe_browsing()`: Integrate with Google Safe Browsing API.
- `get_keyword_value()`: Use `pytrends` to estimate keyword popularity.
- Implementation of caching (LRU cache) and 10s timeouts.
- Error handling and logging.

### [Scoring Component]
#### [NEW] [scoring.py](file:///d:/Công việc iNET/vide code/domain score/scoring.py)
- `calculate_brandability()`: Score based on length and simplicity.
- `calculate_keyword_value()`: Score based on Google Trends data.
- `calculate_authority()`: Score based on OpenPageRank.
- `calculate_age_score()`: Score based on domain age.
- `calculate_tld_score()`: Score based on the top-level domain.
- `apply_penalty()`: Apply Google Safe Browsing penalties.
- `get_star_rating()`: Map final scores to star ratings.

### [UI Component]
#### [NEW] [app.py](file:///d:/Công việc iNET/vide code/domain score/app.py)
- Main Streamlit layout.
- Sidebar for API keys (OpenPageRank, Google Safe Browsing).
- File upload interface.
- Progress bar and status updates using `concurrent.futures`.
- Interactive results table with sorting and filtering.
- Downloadable Excel report with detailed breakdown.

### [Project Meta]
#### [NEW] [requirements.txt](file:///d:/Công việc iNET/vide code/domain score/requirements.txt)
- List all dependencies.

## Verification Plan

### Automated Tests
- I will create a small sample `.csv` and `.xlsx` to test the file processing logic.
- I will mock the API responses to verify the scoring logic without consuming real API credits where possible.

### Manual Verification
1. Run `streamlit run app.py`.
2. Upload a sample file with various domains.
3. Verify normalization logic (www, protocol removal).
4. Enter API keys and verify score calculation.
5. Check filtering and sorting functionality.
6. Download the final report and verify its content.
