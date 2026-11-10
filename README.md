# Family Trip Expense Manager

A shared, mobile-friendly expense tracker.

- Frontend: GitHub Pages (static HTML)
- Database: Google Sheets
- API: Google Apps Script Web App
- Everyone with the link can record an expense.
- Admin PIN protects family/member setup and trip-name changes.
- "Recorded by" and "Paid by" are separate fields.
- Expense shares are split equally among all participants selected for that expense.

## 1. Create the Google Sheet

1. Create a new Google Sheet.
2. Copy the spreadsheet ID from its URL:
   `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit`
3. Open **Extensions → Apps Script**.
4. Replace the contents of `Code.gs` with the supplied `Code.gs`.
5. Set `SPREADSHEET_ID` to your spreadsheet ID.
6. Change `ADMIN_PIN` to a private PIN.
7. Save the script.

The script creates these tabs automatically on first request:
- Settings
- Families
- Members
- Expenses
- Splits

Do not share the Google Sheet with the whole group. The web app runs as the owner.

## 2. Deploy the Apps Script API

1. In Apps Script select **Deploy → New deployment**.
2. Select type **Web app**.
3. Set **Execute as: Me**.
4. Set **Who has access: Anyone**.
5. Deploy and authorize the requested Google permissions.
6. Copy the Web App URL ending in `/exec`.

If you edit the Apps Script later, use **Deploy → Manage deployments → Edit → New version → Deploy**.

## 3. Configure the frontend

1. Open `index.html`.
2. Find:
   `const API_URL = "PASTE_YOUR_APPS_SCRIPT_WEB_APP_URL_HERE";`
3. Replace the placeholder with your Apps Script Web App URL.
4. Save.

## 4. Publish on GitHub Pages

1. Create a GitHub repository, for example `family-trip-expenses`.
2. Upload `index.html` to the repository root.
3. Open **Settings → Pages**.
4. Under Build and deployment, choose **Deploy from a branch**.
5. Choose the `main` branch and `/ (root)` folder.
6. Save. GitHub will provide your public app URL.
7. Share that URL with the family.

## 5. Initial setup

1. Open your GitHub Pages URL.
2. Select **Admin setup**.
3. Enter the admin PIN.
4. Add each family.
5. Add members under the correct family.
6. Share the app link.

Everyone can then open the same link and add transactions. The person entering the transaction selects their own name in "You are recording this expense as". They can select a different person under "Paid by" if they are recording an expense on someone else's behalf.

## Data and access notes

- The app has no member login. Anyone with the link can submit expenses. Do not put highly sensitive information in it.
- Admin PIN only protects admin setup actions. It is a shared PIN, not individual identity verification.
- Anyone with the link can choose any name in the recorder field. The app records the selected name, not verified identity.
- Keep the Google Sheet private. The Apps Script web app accesses it as the owner.
- Back up the Google Sheet periodically.
- CSV exports are available in the Settlement tab.
- This version supports equal splitting among everyone or equal splitting among a selected subset. It does not yet support different custom amounts or percentages per participant.

## Troubleshooting

**"Add your deployed Apps Script URL"**  
Set `API_URL` in `index.html`, commit and push.

**"Could not load data from Google Sheets"**  
Check that the Web App deployment is active, access is set to Anyone, and the URL ends in `/exec`.

**You changed Code.gs but the app still behaves the same**  
Create a new deployment version in Apps Script and deploy it. Keep using the current `/exec` URL if editing the existing deployment.

**Admin PIN rejected**  
Check `ADMIN_PIN` in Code.gs, deploy a new version, and re-enter the PIN in the Admin setup tab.
