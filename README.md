# PakWheels Vehicle Dataset Scraper

A Python scraper that collects every used car listing from [PakWheels.com](https://www.pakwheels.com) and builds a structured dataset with full specs, seller details, and downloaded images.

## Features

- Scrapes all paginated search results (800–1000+ pages)
- Visits each listing's detail page to extract complete specs
- Downloads all gallery images per listing
- Saves data incrementally — safe to stop and resume anytime
- Outputs a clean CSV ready for analysis or ML pipelines

## Dataset Fields

| Group | Fields |
|---|---|
| Listing | title, price, location, year, mileage, fuel_type, engine_cc, transmission, last_updated |
| Detail | registered_in, color, assembly, engine_capacity, body_type, ad_ref |
| Seller | seller_info, seller_phone, posted_date |
| Images | image_urls, image_count, images_downloaded |

## Output
```
pakwheels_vehicles.csv     ← full dataset
pakwheels_images/
    10833561/
        01.webp
        02.webp
        ...
    11246911/
        01.webp
        ...
```

## Installation
```bash
pip install requests beautifulsoup4 pandas
```

## Usage
```python
# In Jupyter Notebook

# Step 1 — verify selectors are working
diagnose()

# Step 2 — run full scrape (resume=True picks up if interrupted)
df = scrape_pakwheels(
    max_pages=None,        # None = all pages
    download_imgs=True,
    scrape_details=True,
    output_file="pakwheels_vehicles.csv",
    resume=True,
)
```

For a quick test run, set `max_pages=3`.

## Notes

- A full scrape takes approximately 12–15 hours due to polite rate limiting (2s delay between requests)
- The CSV is saved after every page so interrupted runs can be resumed without data loss
- Images are saved to `pakwheels_images/<listing_id>/` and skipped if already downloaded

## Disclaimer

This project is intended for personal research and educational use only. Please review PakWheels' terms of service before scraping at scale. Do not use the collected data for commercial purposes.
