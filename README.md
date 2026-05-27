# Kenya Pharmacy And Poisons Board — Retail Facilities Scraper

A Jupyter Notebook that scrapes the names and counties of all licensed retail pharmacy facilities listed on the [Pharmacy & Poisons Board of Kenya](https://practice.pharmacyboardkenya.org/LicenseStatus?register=facilities&ftype=retail) public register, and saves the results to a CSV file.

---

## What It Does

1. Launches a Chrome browser using `undetected-chromedriver` to bypass bot detection.
2. Navigates to the PPB public register filtered for **retail facilities**.
3. Iterates through every page of results (up to 500 pages).
4. For each facility row, clicks **View Details** to open a modal and extracts the **county** from the modal content.
5. Falls back to parsing the county from the facility name (e.g. `Facility Name (County)`) if the modal method fails.
6. Saves all collected data to `retail_facilities_name_county.csv`.
7. Prints a summary of the top 10 counties by facility count.

---

## Output

A CSV file — `retail_facilities_name_county.csv` — with two columns:

| Column | Description |
|---|---|
| `Facility Name` | Name of the licensed retail pharmacy |
| `County` | County where the facility is located |

---

## Requirements

- Python 3.8+
- Google Chrome (version 145 or compatible)

Install dependencies:

```bash
pip install undetected-chromedriver selenium pandas
```

---

## Usage

1. Clone the repository and open the notebook:

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
jupyter notebook scrapper.ipynb
```

2. Run all cells in order. Chrome will launch automatically and begin scraping.

3. When complete, `retail_facilities_name_county.csv` will be saved in the same directory.

> **Note:** The scraper runs in non-headless mode by default (a browser window will open). To run headlessly, uncomment `options.add_argument("--headless=new")` in the config cell.

---

## Configuration

At the top of the main cell you can adjust these settings:

| Variable | Default | Description |
|---|---|---|
| `OUTPUT_FILE` | `retail_facilities_name_county.csv` | Output file name |
| `MAX_PAGES` | `500` | Maximum pages to scrape (safety limit) |
| `DELAY_AFTER_CLICK` | `3s` | Wait time after clicking View Details |
| `DELAY_AFTER_CLOSE` | `2s` | Wait time after closing a modal |
| `DELAY_AFTER_PAGE` | `5s` | Wait time after navigating to the next page |

---

## Notes

- The scraper uses `undetected-chromedriver` to avoid being blocked by the site's bot-detection.
- If the modal does not contain a clearly labelled county field, the scraper attempts to extract the county from parentheses in the facility name.
- Delays are intentionally conservative to avoid overloading the server. Please scrape responsibly.

---

## License

MIT
