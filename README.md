# CAISO-EnergyStorage

This repository contains code and data relating to _Comparative Withholding Behavior Analysis of Historical Energy Storage Bids in California_.

<b>Authors:</b> Neal Ma, Ningkun Zheng, Ning Qi, Bolun Xu

## Repository Structure

The repository is structured as follows:

- `src/`: primary directory containing notebooks, data, and figures
  - `data/`: directory containing all processed data
    - `DAP_CSV/`: day-ahead price `csv` files in CAISO from LCG Consulting
    - `ES_BIDS/CAISO_ES_BIDS.parquet`: scraped energy storage bids from _CAISO Daily Energy Storage Reports_
    - `CAISO_DAP.csv`: day-ahead CAISO prices from LCG Consulting in a single `csv` file
    - `CAISO_DAP.parquet`: same as above but in a `parquet` file
    - `CAISO_RTP.csv`: real-time CAISO prices from LCG Consulting in a single `csv` file
    - `CAISO_RTP.parquet`: same as above but in a `parquet` file
    - `optimal_bids.csv`: optimal generated bids
  - `figures/`: directory containing all figures included in the report
  - `CAISO_ES_BID_FINAL_ANALYSIS.ipynb`: final analysis and figure generation
  - `CAISO_ES_BID_SCRAPING.ipynb`: scrapes data from _CAISO Daily Energy Storage Reports_ and saves to `data/ES_BIDS/CAISO_ES_BIDS.parquet`
  - `CAISO_ES_OPTIMAL_BIDS.ipynb`: generates optimal bids from real-time data and saves to `data/optimal_bids.csv`
  - `key.md`: variable labels and definitions for data in `data/ES_BIDS/CAISO_ES_BIDS.parquet`

## Instructions

These notebooks should be ready-to-run out of the box in the following order:

1. `CAISO_ES_BID_SCRAPING.ipynb`: Scrape new bid data (if you would like more updated data than available here). You may need to adjust this if the format of _CAISO Daily Energy Storage Reports_ change
2. `CAISO_ES_OPTIMAL_BIDS.ipynb`: Generate optimal bids using `data/CAISO_RTP.csv`, `data/CAISO_DAP.csv`, and `data/ES_BIDS/CAISO_ES_BIDS.parquet`. These files need to updated if more recent data is desired
3. `CAISO_ES_BID_FINAL_ANALYSIS.ipynb`: Generate plots and carry out statistical analyses. You can directly run this notebook if you want to use the same data used in the report

## Contact

Any questions about the code can be directed to Neal Ma (@nmadev on github)