POSTMAN — WHAT IT IS AND HOW TO INSTALL IT

1. What Postman is
   Postman is a tool for testing and interacting with APIs. Instead of
   writing curl commands in a terminal or wiring up test code, it gives
   you a GUI to send HTTP requests (GET, POST, PUT, DELETE, etc.),
   inspect responses, save request collections, set up environments
   (dev/staging/prod variables), and write automated test scripts
   against your endpoints.

2. Installation options

   OPTION A: Desktop app (Windows/Mac/Linux) — simplest for local dev
   - Download the installer from the official site:
     https://www.postman.com/downloads/
   - Run the installer for your OS.
   - It installs as a standalone desktop app with an account login
     (for syncing collections across devices).

   OPTION B: Via package manager (Linux/Mac/Windows)
```bash
sudo snap install postman          # Linux
brew install --cask postman        # macOS
winget install Postman.Postman     # Windows
```
   These install the same desktop app without manually downloading
   and running an installer file.

   OPTION C: Web version (no install)
   - Go to https://web.postman.co in your browser.
   - Runs directly in-browser, syncs with your Postman account.
   - Useful if you don't want anything installed locally, though it
     has fewer capabilities than the desktop app (e.g. no local proxy
     capture).

3. After installing
   - On first launch, Postman asks you to sign in or create an
     account (this enables syncing collections/environments across
     devices — you can also skip and use it offline in limited mode).
   - You then create a "Request": click New → HTTP Request, enter a
     URL and method (GET/POST/etc.), and hit Send to see the response.

4. Which option to pick
   - Just working locally on your own machine → Option A (desktop app)
     is easiest, most full-featured.
   - Already comfortable with your OS's package manager → Option B
     gets you the same app faster via one command.
   - Want zero install, quick one-off testing → Option C (web version).