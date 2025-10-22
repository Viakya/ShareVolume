# Overview
This single-page web app fetches the SEC XBRL Company Concepts data for EntityCommonStockSharesOutstanding and visualizes the maximum and minimum reported shares for fiscal years greater than 2020.

It:
- Fetches APA Corporation (CIK 0001841666) by default directly from the SEC endpoint.
- Computes and displays the max/min values for FY > 2020.
- Exposes a Download data.json action containing exactly:
  {"entityName": "...", "max": {"val": ..., "fy": "..."}, "min": {"val": ..., "fy": "..."}}
- Supports dynamic company switching using the URL query parameter ?CIK=########## (10 digits). When provided, it uses a proxy (AIPipe/Jina) to fetch the SEC endpoint and updates the page live.

Note on SEC guidance: From browsers, setting a custom User-Agent header is restricted; server-side usage should follow SEC’s guidance. This app uses a direct fetch for the default case and a proxy for alternate CIKs to handle CORS/UA limitations.

# Setup
No build tools required.

- Save the provided index.html file.
- Optionally host it on any static server (GitHub Pages, Netlify, local file system, etc.).

Files expected in the repository (for final submission):
- index.html (this app)
- uid.txt (provided as attachment; include it exactly as-is)
- LICENSE (MIT License text)
- data.json (optional to commit if you run the app and download it)

# Usage
- Default APA view:
  - Open index.html
  - The app fetches https://data.sec.gov/api/xbrl/companyconcept/CIK0001841666/dei/EntityCommonStockSharesOutstanding.json
  - It then shows:
    - Title and H1 with the live entity name (APA Corporation)
    - Max/min values (FY > 2020) with the required element IDs:
      share-entity-name,
      share-max-value, share-max-fy,
      share-min-value, share-min-fy
- Alternate company:
  - Open index.html?CIK=0001018724 (or any other 10-digit CIK)
  - The app fetches via a proxy (AIPipe/Jina) and dynamically updates all fields and the title.

Export:
- Click “Download data.json” to save the computed JSON locally in the exact required structure. You can commit this file to the repo if needed.