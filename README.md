# Corporate_Network_Analysis

This project analyzes corporate sponsorship and partnership networks using web scraping, automated querying, and social network analysis (SNA). The goal is to uncover both direct and indirect relationships among organizations using data extracted from websites and search results.

---

## 🚧 Project Pipeline

### Step 1: Homepage Hyperlink Extraction
**Notebook**: `1_Hyperlink_Home.ipynb`  
- Crawl each organization's homepage.  
- Extract internal and external hyperlinks.  
- Identify direct links to known partners.  

---

### Step 2: Sponsor List Cleaning
**Notebook**: `2_Sponsor_List_Cleaner.ipynb`  
- Standardize sponsor names.  
- Normalize variations (e.g., acronyms, short names).  
- Remove noise and duplicates.  

---

### Step 3: Partner Connection Mining
**Notebooks**:
- `3_Hyperlink.ipynb`: Checks if two organizations link to each other from their websites.  
- `3_Google_Search.ipynb`: Uses automated Google Search to detect name mentions.  

---

### Step 4: Final Connection List Generation
**Notebook**: `4_Create_Final_List.ipynb`  
- Merges Google and hyperlink results.  
- Optionally filters weak signals.  
- Produces the final edge list.  

---

### Step 5: Result Visualization & Analysis
**Notebook**: `5_Result_Analysis.ipynb`  
- Builds SNA graphs using NetworkX.  
- Outputs include:
  1. **Basic Graph** – raw connection network  
  2. **Colored Graph** – node types and degrees visualized  
  3. **Simplified Graph** – shows interaction between org types  

---

## 📄 Methodology Summary

- **Input Sources**:
  - Organization homepages
  - Annual reports, posts, or articles
- **Connection Types**:
  - `Google_text_mentioned`: Detected via keyword presence using Google  
  - `Hyperlink_mentioned`: Confirmed through direct hyperlinks  
- **Output Metrics** (see `Sample report.pdf`):
  - Total unique partners
  - Connection breakdown by method
  - Node type distribution (e.g., business, nonprofit)

---

## 🧪 Sample Output

Refer to the provided `Sample report.pdf`, which includes:
- Summary statistics for a masked corporate  
- Total connections and breakdown  
- Organization type distribution  
- Graphical network visualizations

---

## 📦 Dependencies

- `requests`, `bs4`, `re`, `tqdm`  
- `pandas`, `numpy`  
- `NetworkX`, `matplotlib`  
- Google Custom Search API (optional)

---

## 📌 Notes

- All analysis assumes each organization has a unique, functional homepage.  
- Network edges are undirected.  
- False positives in Google-based connections are retained for recall maximization.  
- To avoid IP bans and 443 Bad Gateway errors from Google Search, we deployed scraping scripts on AWS EC2 instances.  
  - As noted in `3_Google_Search.ipynb`:  
    > *"To solve the problem, I switched to a different AWS machine (IP rotation), and the error was resolved. This is helpful if the machine is blocked by Google or returns error code 443 due to automation detection."*  
  - Restarting EC2 instances dynamically refreshes the public IP, enabling continued scraping without third-party proxies.