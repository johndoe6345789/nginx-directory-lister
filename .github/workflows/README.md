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
4. Logs in to Docker Hub
5. Extracts metadata for tagging
6. Builds and pushes multi-platform images (amd64, arm64)

**Required Secrets:**
- `DOCKER_USERNAME`: Docker Hub username
- `DOCKER_PASSWORD`: Docker Hub password or access token

**Tags Generated:**
- Semantic version tags (e.g., `1.0.0`, `1.0`, `1`)
- `latest` tag for releases from the default branch

## Setting Up Secrets

To use the release workflow, configure the following secrets in your repository settings:

1. Go to: Settings → Secrets and variables → Actions
2. Add the following repository secrets:
   - `DOCKER_USERNAME`: Your Docker Hub username
   - `DOCKER_PASSWORD`: Your Docker Hub password or personal access token

## Manual Release

You can trigger a release manually:
1. Go to Actions → Release workflow
2. Click "Run workflow"
3. Select the branch
4. Click "Run workflow"
