# Chintaporadh Source Content

This repository serves as the headless CMS/Database for the Chintaporadh article website. It follows a Git-CMS architecture.

## Structure

- **`global.json`**: The central index of all articles. Contains summary data for listing articles on the frontend.
- **`articles/{UID}/`**: Individual article folders.
  - **`content.md`**: The article body in Markdown.
  - **`metadata.json`**: Detailed metadata for the specific article.
  - **`images/`**: Assets related to the article.

## Usage

### 1. CDN Access (Public)
To fetch content in your frontend application, use a CDN service like **jsDelivr**.

**Base URL:**
```
https://cdn.jsdelivr.net/gh/{GITHUB_USERNAME}/{REPO_NAME}@main
```

**Examples:**
- Fetch Global Index: `https://cdn.jsdelivr.net/gh/user/repo@main/global.json`
- Fetch Article Cover: `https://cdn.jsdelivr.net/gh/user/repo@main/articles/cJjpTZsYwk_9/images/cover.png`
- Fetch Article Content: `https://cdn.jsdelivr.net/gh/user/repo@main/articles/cJjpTZsYwk_9/content.md`

### 2. Admin API Access (Private/Auth)
To manage content programmatically (Admin Panel), use the **GitHub REST API**.

**Endpoint:** `https://api.github.com/repos/{OWNER}/{REPO}/contents/{PATH}`

**Authentication:**
- Requires a **Personal Access Token (PAT)** or OAuth token with `repo` scope.

**Workflow:**
1. **Read**: GET request to the file path to retrieve `sha` and `content` (base64 encoded).
2. **Update**: PUT request to the file path with updated content (base64) and the correct `sha`.
3. **Create**: PUT request to a new path.
4. **Delete**: DELETE request.

### Adding a New Article
1. Generate a unique ID (NanoID 12 chars recommended).
2. Create folder `articles/{UID}`.
3. Add `content.md` and `metadata.json`.
4. Update `global.json` with the new entry.
5. Commit and Push.
