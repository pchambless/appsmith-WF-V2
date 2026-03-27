# appsmith-WF-V2

The Whatsfresh Appsmith Prototype for Version 2

This repository stores the source for a [Appsmith](https://www.appsmith.com/) application using
Appsmith's built-in Git integration. All pages, queries, datasources, and JS objects are
version-controlled here as JSON files that Appsmith reads and writes automatically.

---

## Connecting your Appsmith app to this repository

Follow these steps to attach your existing Appsmith application (running on Digital Ocean) to
this GitHub repository.

### Prerequisites

- You must be an **Administrator** or have **Create Application** permission in the Appsmith
  workspace.
- The Appsmith instance must have outbound internet access to reach GitHub over SSH (port 22).
- You need **write access** to this GitHub repository so you can add a deploy key.

---

### Step 1 — Copy this repository's SSH URL

1. Open this repository on GitHub.
2. Click the green **Code** button.
3. Select the **SSH** tab and copy the URL (it looks like
   `git@github.com:pchambless/appsmith-WF-V2.git`).

---

### Step 2 — Open Git settings in Appsmith

1. Navigate to your Appsmith application on your Digital Ocean droplet
   (e.g. `http://<your-droplet-ip>`).
2. Open the application you want to connect.
3. In the bottom-left corner of the editor, click the **Connect Git** button
   (looks like a branch/git icon).
4. When prompted for a Git hosting provider, select **GitHub**.

---

### Step 3 — Enter the repository URL and generate SSH keys

1. Paste the SSH URL you copied in Step 1 into the **Remote URL** field.
2. Click **Generate SSH Keys**.
3. Appsmith will display two public keys — an **ECDSA 256** key and an **RSA 4096** key.
4. Copy the key you want to use (RSA 4096 is the safer default choice).

> **Important:** Only SSH connections are supported. HTTPS remote URLs will not work.

---

### Step 4 — Add the deploy key to this GitHub repository

1. Go to this repository on GitHub:
   `https://github.com/pchambless/appsmith-WF-V2`
2. Click **Settings** → **Deploy keys** → **Add deploy key**.
3. Fill in the form:
   - **Title:** e.g. `Appsmith Digital Ocean`
   - **Key:** paste the public key you copied from Appsmith
   - **Allow write access:** ✅ check this box (required so Appsmith can push commits)
4. Click **Add key**.

---

### Step 5 — Connect and initialize

1. Return to Appsmith and click **Connect Git** (or **Connect** / **Save** depending on your
   Appsmith version).
2. Appsmith will perform an initial commit that pushes your application's current state to this
   repository as structured JSON files.
3. Once the connection succeeds you will see a branch selector and Git controls at the bottom of
   the editor.

---

## Working with Git in Appsmith

| Action | How |
|--------|-----|
| **Commit changes** | Click the Git icon → **Commit & Push** |
| **Pull latest changes** | Click the Git icon → **Pull** |
| **Create / switch branch** | Click the branch name in the bottom bar |
| **Discard local changes** | Click the Git icon → **Discard** |

---

## Repository structure (after first commit)

Appsmith populates this repository automatically. The typical layout is:

```
appsmith-WF-V2/
├── application.json        # Top-level app configuration and metadata
├── pages/
│   ├── Page1/
│   │   └── Page1.json      # Widgets, layout, queries per page
│   └── ...
├── datasources/
│   └── *.json              # Datasource configs (credentials are NOT stored here)
├── queries/
│   └── *.json
├── jsobjects/
│   └── *.json
├── theme.json              # App theme settings
├── .gitignore
└── README.md
```

> **Security note:** Appsmith never stores datasource credentials or secrets in the repository.
> After importing the app on a new Appsmith instance you will need to re-enter connection
> credentials for each datasource.

---

## Importing this repository into a new Appsmith instance

If you want to spin up the application from this repository on a fresh Appsmith instance:

1. In Appsmith, go to your workspace home page.
2. Click **Import** → **Import from Git repository**.
3. Paste the SSH URL (`git@github.com:pchambless/appsmith-WF-V2.git`).
4. Follow Steps 3–5 above to generate and add a new deploy key.
5. Reconnect any datasources when prompted.

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| "Host key verification failed" | Make sure port 22 is open outbound from your droplet and that GitHub's SSH fingerprint is trusted. |
| "Repository is not empty" error | The repository must contain only files Appsmith recognizes (or be completely empty before the first connect). Remove any conflicting files and retry. |
| Deploy key permission error | Ensure **Allow write access** is checked on the deploy key in GitHub Settings → Deploy keys. |
| Changes not showing after pull | Use **Discard** to clear any local conflicts, then pull again. |

---

## Resources

- [Appsmith Git integration docs](https://docs.appsmith.com/advanced-concepts/version-control-with-git/guides/setup-github)
- [Appsmith self-hosting on Digital Ocean](https://docs.appsmith.com/getting-started/setup/installation-guides/digitalocean)
- [Appsmith community forum](https://community.appsmith.com/)
