# GitHub Workflows

This repository includes two GitHub Actions workflows for automated builds and releases.

## CI Workflow

**File:** `.github/workflows/ci.yml`

**Triggers:**
- Push to `main` branch
- Pull requests to `main` branch

**Actions:**
1. Checks out the code
2. Sets up Docker Buildx
3. Builds the Docker image using `make build`
4. Tests the Docker image by:
   - Creating a test volume with sample content
   - Running the container
   - Verifying the container is running
   - Testing HTTP response from the web server
   - Cleaning up test resources

## Release Workflow

**File:** `.github/workflows/release.yml`

**Triggers:**
- GitHub releases (when published)
- Manual workflow dispatch

**Actions:**
1. Checks out the code
2. Sets up QEMU for multi-platform builds
3. Sets up Docker Buildx
4. Logs in to GitHub Container Registry (ghcr.io)
5. Extracts metadata for tagging
6. Builds and pushes multi-platform images (amd64, arm64)

**Authentication:**
- Uses the built-in `GITHUB_TOKEN` for authentication
- No additional secrets required
- Requires `packages: write` permission

**Tags Generated:**
- Semantic version tags (e.g., `1.0.0`, `1.0`, `1`)
- `latest` tag for releases from the default branch

**Image Location:**
- Images are pushed to: `ghcr.io/<owner>/<repo>`
- Example: `ghcr.io/johndoe6345789/nginx-directory-lister`

## Setting Up Secrets

The release workflow uses GitHub's built-in `GITHUB_TOKEN` and does not require any additional secrets to be configured.

## Manual Release

You can trigger a release manually:
1. Go to Actions → Release workflow
2. Click "Run workflow"
3. Select the branch
4. Click "Run workflow"
