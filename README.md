# V2G Trial Map

An interactive mind map of what the Vehicle-to-Grid trial has taught us. It reads a Google Sheet and refreshes every 5 minutes, so new rows appear without anyone touching this code.

Live site: https://rewiring-nz.github.io/v2g-map/

## Connecting the Google Sheet

1. In Google Sheets, open **File → Share → Publish to web**.
2. Choose the **Entries** tab and **Comma-separated values (.csv)**, then click **Publish**.
3. Copy the link. In `index.html`, paste it into `sheetCsvUrl` near the top of the script:

   ```js
   const CONFIG = {
     sheetCsvUrl: "https://docs.google.com/spreadsheets/d/e/.../pub?gid=...&single=true&output=csv",
     refreshMinutes: 5,
   };
   ```

4. Commit the change. GitHub Pages updates the site within a minute or two.

Until a link is set, or if the sheet can't be loaded, the map shows built-in sample data and says so in the header.

Anyone with the published link can read the published tab, so keep private household details out of it.

## Sheet columns

Headers are matched by name, in any order and any case. Extra columns are ignored.

| Column | Also recognised as | Notes |
|---|---|---|
| Title | Name, Headline | Required. Rows without a title are skipped |
| Top tag | Topic, Category | Becomes a branch of the map. Blank goes under "Uncategorised" |
| Type of entry | Type | Issue, Learning, or Explainer/Educational. Anything else counts as Learning |
| Status | | Open or Resolved, for issues only. Blank counts as Open |
| Description | Summary | Shown in the side panel |
| Article | Body | Longer text, shown under "Article" in the side panel |
| Tags | Keywords | Comma-separated, searchable and clickable |
| Contributors | Added by, Author | Shown as "Added by" |
| Image | Photo | A web link to an image (pictures pasted into cells don't come through) |
| Related | Links | IDs or exact titles of other rows, comma-separated |
| ID | | Short code that Related can point to |
| Link | URL | URL of the full article, e.g. in Outline |

Headers only need to contain the key word, so "Description long form text" counts as Description.

## Editing the map

Everything lives in `index.html`: no build step. It uses [d3](https://d3js.org/) from cdnjs.
