# CAISO Energy Storage Bid Data Label Key

This page describes the data produced by <code>CAISO_ES_BID_SCRAPING.ipynb</code> including specifications about temporal resolution, bid segments, and more. Original data are scraped from the [CAISO Daily Energy Storage Reports](https://www.caiso.com/library/daily-energy-storage-reports). This data is best understood through the [CAISO 2023 Special Report on Battery Storage](https://www.caiso.com/documents/2023-special-report-on-battery-storage-jul-16-2024.pdf).

The data stored in <code>data/ES_BIDS/CAISO_ES_BIDS.parquet</code> is a table with `datetime` as the index and all other columns as defined in [Feature Definitions and Specifications](#feature-definitions-and-specifications).

## Abbreviation and Term Definitions


| Code  | Description          |
|-------|----------------------|
| `tot` | Total |
| `AS`  | Ancillary Services |
| `Bid` | Bid |
| `energy` | Energy in MW |
| `charge` | State of Charge in MWh |
| `hybrid` | Hybrid resources (i.e. storage + renewables being treated as a single source) |
| `neg` | Negative values |
| `pos` | Positive values |
| `ru`  | Regulation Up - An Ancillary Service (AS) for CAISO operation in a capacity market for the instant <b>increase</b> in operating level |
| `rd`  | Regulation Down - An Ancillary Service (AS) for CAISO operation in a capacity market for the instant <b>decrease</b> in operating level |
| `sr`  | Spinning Reserves - Available generation that is running and capable of <b>ramping within 10 minutes</b> and <b>running for at least 2 hours</b> |
| `nr`  | Non-Spinning Reserves - Available generation that is not running but can <b>ramp and be synchronized within 10 minutes</b> |
| `ifm` | Integrated forward market - Day-ahead unit commitment and congestion management market |
| `ruc` | Residual unit commitment - Reliability function to account for the different in the projected and real demand in CAISO with shorter commitment instruction horizons |
| `rtpd`| Real-time pre-dispatch (?) |
| `rtd` | Real-time dispatch (?) |
| `fmm` | Fifteen-minute market - Fifteen minute market scheduling in the day-ahead market |
| `ss`  | Self schedule - Self-scheduled battery operation (charge/discharge) |

Definitions sourced from these resources:
- https://www.caiso.com/documents/2023-special-report-on-battery-storage-jul-16-2024.pdf
- https://www.caiso.com/documents/whitepaper-priceperformanceanalysis-apr3-2019.pdf
- https://www.caiso.com/Documents/2210.pdf

## Feature Definitions and Specifications

| Column | Description | Granularity |
|--------|-------------|-------------|
| <b>Battery Resources</b> | | |
| `tot_energy_{ifm,ruc,rtpd,rtd}` | Total Energy Awards | 5 minutes |
| `tot_charge_{ifm,ruc,rtpd,rtd}` | Total State of Charge | 5 minutes |
| `as_{ru,rd,sr,nr}_ifm` | IFM AS Awards | 1 hour |
| `as_{ru,rd,sr,nr}_rtpd` | FMM AS Awards | 15 minutes |
| `bid_ifm_{pos,neg}_{ss,1,...,11}` | IFM Energy Bid in Capacity - Discharge (+) / Charge (-) | 1 hour |
| `bid_rtpd_{pos,neg}_{ss,1,...,11}` | FMM Energy Bid in Capacity - Discharge (+) / Charge (-) | 15 minutes |
| <b>Hybrid Resources</b> | | |
| `tot_energy_hybrid_{ifm,ruc,rtpd,rtd}` | Total Energy Awards | 5 minutes |
| `tot_charge_hybrid_{ifm,ruc,rtpd,rtd}` | Total State of Charge | 5 minutes |
| `as_{ru,rd,sr,nr}_hybrid_ifm` | IFM AS Awards | 1 hour |
| `as_{ru,rd,sr,nr}_hybrid_rtpd` | FMM AS Awards | 15 minutes |
| `bid_ifm_{pos,neg}_hybrid_{ss,1,...,11}` | IFM Energy Bid in Capacity - Discharge (+) / Charge (-) | 1 hour |
| `bid_rtpd_{pos,neg}_hybrid_{ss,1,...,11}` | FMM Energy Bid in Capacity - Discharge (+) / Charge (-) | 15 minutes |

#### Bid Segment Labels

Bid segments from the table above are defined below.

| Suffix  | Description/Range |
|---------|-------------------|
|   `ss`  | Self Schedule |
|   `1`   | `[-150, -100]` |
|   `2`   | `(-100, -50]` |
|   `3`   | `(-50, -15]` |
|   `4`   | `(-15, 0]` |
|   `5`   | `(0, 15]` |
|   `6`   | `(15, 50]` |
|   `7`   | `(50, 100]` |
|   `8`   | `(100, 200]` |
|   `9`   | `(200, 500]` |
|   `10`  | `(500, 1000]` |
|   `11`  | `(1000, 2000]` |