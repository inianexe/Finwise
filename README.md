# Finwise

Finwise is a mobile-friendly personal finance app with local accounts, private SQLite storage, and optional AI insights powered by the installed Codex CLI.

## Start and preview

From this folder, run:

```bash
python3 server.py
```

Enter **http://localhost:8000** in your VS Code mobile preview extension. Set its width to about 390 px for the phone layout. Use `FINWISE_PORT=8001 python3 server.py` if port 8000 is already occupied.

The plain `python3 -m http.server` command no longer works for this app: login, saved data, and AI insights require `server.py`.

## First use

Choose **Create an account**, then enter your name, email, and a password of at least 12 characters. Your financial records are saved under that account in `.data/finwise.sqlite3`. Another account on the same computer cannot read them. Sessions use an HTTP-only cookie and expire after 30 days. The server listens on localhost only. Export your transactions regularly if you need a backup. There is no password reset or cloud sync yet.

If you entered real data in the earlier browser-only version, Finwise offers to import it after you sign in. Sample data is never imported.

## Features

- Add income and expenses, create custom expense categories, and see the six-month cash-flow chart.
- Import CSV bank statements with date, description, and amount or debit/credit columns. Review detected entries before import.
- Scan a receipt photo in the browser. Tesseract.js is downloaded from a CDN on first use, so scanning needs internet. Review detected details before saving.
- Track savings goals and monthly category limits. The bell shows categories above 80% of their limit.
- Download a monthly HTML report that can be printed to PDF and export all transactions as CSV.
- Use **AI insights** for a Codex CLI analysis. It sends six months of totals, category spending, limits, and goal amounts to Codex. Names, merchant descriptions, and email addresses stay out of that analysis. It requires the CLI to be installed, logged in (`codex login status`), and able to reach OpenAI. Codex usage may count against your account limits.

The AI analysis is generated only when you press **Analyze my finances**. It can be inaccurate and is for budgeting reflection, not financial advice.

## Project files

- `server.py` — local HTTP server, account authentication, SQLite storage, and Codex invocation.
- `insight-schema.json` — required shape of Codex's analysis response.
- `index.html` — app screens, login, navigation, and dialogs.
- `styles.css` — responsive layout and styling.
- `app.js` — UI, calculations, imports, notifications, and report downloads.
- `.data/` — private SQLite database, created on first start and excluded from Git.

The broader ideas in `req.txt`, such as predictions, a what-if simulator, and gamification, remain future-version work.
