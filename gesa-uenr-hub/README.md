# GESA-UENR Academic Resource Hub

A free static website (HTML, CSS, vanilla JS). No server, no paid service, no domain to buy. All content lives in JSON files.

## 1. Put it online (GitHub Pages)
1. Create a free account at github.com, click **New repository**, name it `gesa-uenr-hub`, set it to **Public**.
2. Click **uploading an existing file**, drag in everything from this folder (keep the folders), then **Commit changes**.
3. Go to **Settings > Pages**. Under **Branch** choose `main` and `/ (root)`, then **Save**.
4. After 1 to 2 minutes your site is at `https://<your-username>.github.io/gesa-uenr-hub/`. Share that link.

## 1b. No-code uploads (recommended): Google Drive + Google Sheet
Do this once. Afterwards you never touch GitHub to add materials.
1. **Drive folder:** at drive.google.com create a folder `GESA Materials`. Right-click it > **Share** > General access > **Anyone with the link** (Viewer). Copy its link.
2. **Materials sheet:** go to sheets.new. **File > Import > Upload**, choose `sheet-templates/materials-template.csv`, pick **Replace spreadsheet**. Rename the tab to `Materials`. Delete the two example rows. Then **File > Import**, upload `forms-template.csv`, pick **Insert new sheet(s)**, and rename that tab `Forms`.
3. **Publish each tab:** **File > Share > Publish to web**. Choose the `Materials` tab and format **Comma-separated values (.csv)**, click **Publish**, copy the link. Repeat for the `Forms` tab. Also copy the normal address-bar link of the sheet.
4. **Tell the site (one small edit):** on GitHub open `data/site.json`, click the pencil, and paste the links between the quotes: `resourcesCsv` (Materials CSV link), `formsCsv` (Forms CSV link), `driveFolderUrl` (folder link), `sheetEditUrl` (sheet address-bar link). Commit.
5. **Add a material from now on:** upload the file to the Drive folder from your phone or computer. Right-click it > **Share** > **Copy link**. In the Materials sheet add a row and paste the link in the **Link** column. Refresh the site after a minute or two.

Column tips: Programme can be the plain name (Petroleum Engineering). Level is 100/200/300/400. Semester is 1 or 2. Category is Lecture Slides, Reference, Past Questions or Tutorial. Exam Type is Mid-semester or End-of-semester. File Type is pdf, pptx or docx. Date Added (like 2026-10-23) feeds "Recently added".
**Google Forms:** create the form at forms.google.com as usual, click **Send > link icon**, copy, and add a row in the `Forms` tab. Set Status to Open or Closed.
Only people you share the Sheet and Drive folder with as **Editor** can add materials.

**Sample content:** the site ships with 3 SAMPLE materials and 1 SAMPLE form (they point to example.com). To remove them, open `data/resources.json` and `data/forms.json` on GitHub, clear what is inside `"items": [ ]`, and commit.

## 2. Folder layout
- `data/programmes.json` the 2 schools and 8 programmes
- `data/courses/<programme>.json` courses per level and semester (Petroleum Level 100 Sem 1 is filled in)
- `data/resources.json` every slide, book, past question and tutorial
- `data/links.json`, `books.json`, `forms.json`, `cv.json`, `site.json` the other pages
- `materials/<programme>/<level>/<semester>/<COURSE>/<category>/` your PDF and PPT files
- `admin.html` the Admin Helper

## 3. Add materials from your phone or computer (no code)
1. One time: open `admin.html` on your live site and follow **1. Connect to your GitHub** (create a fine-grained token limited to this repo with Contents read/write, then save).
2. **Upload material** tab: choose programme, level, semester, course, category, type a title, pick the file from your device, tap **Publish**. The file and the list entry are saved to GitHub for you.
3. Wait 1 to 2 minutes and refresh the site.

**Files over 25 MB:** upload to Google Drive, share as "Anyone with the link", and paste the link in the external link box instead of choosing a file.

**File naming** is automatic: `COURSECODE_Category_Lecturer_Year.ext`, for example `MATH109_Slides_DrAsante_2026.pdf`.

**Manage materials** tab: edit a title or delete a material (its file is removed too).
**Forms** tab: tap *Create a new Google Form*, build it on Google, copy the link, paste it to list it on the Forms page, close or remove it later.
**Courses** tab: add courses to any programme, level and semester.

## 4. Add courses
Open `data/courses/<programme>.json` and add `{ "code": "MATH 109", "name": "Engineering Mathematics I", "credits": 3 }` inside the right `level-X` > `sem-X` list. Empty lists show "Materials coming soon".

## 6. Forms, links, books, CV templates
Edit `forms.json`, `links.json`, `books.json`. For CV templates, upload the DOCX/PDF to `materials/templates/` and put its path in the `url` of `cv.json`.

## 7. Security, honestly
Anyone can open `admin.html`, but nothing changes without a valid GitHub token, and the token only works for people you trust. **Real access control is GitHub.** Keep the token private, set an expiry, and revoke it in GitHub settings if lost. Other committee members need their own token and must be added under Settings > Collaborators.

## 8. Other notes
- Dark/light mode and last-visited page are remembered in the browser. There is no tracking and no analytics.
- Installable as an app (PWA) and works offline for pages already visited.
- Decap CMS was left out on purpose: it needs an extra login server to work reliably on GitHub Pages.
- Not included yet: QR codes for forms, template thumbnails. Share form links directly or generate QR codes with any free QR tool.
