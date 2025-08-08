# TikTok Viral Pro Shared - Whisper Binaries Release Guide

This guide explains how to manage and release new versions of the pre-compiled Faster-Whisper binaries. These binaries are large and are not tracked directly in the Git repository; instead, they are distributed via GitHub Releases as assets.

## 1. Updating Local Whisper Binaries

When new versions of the Whisper binaries are available, replace the existing files in the `whisper/` directory with the new ones.

The files are:

- `whisper/Faster-Whisper-XXL_r245.4_linux.7z`
- `whisper/Faster-Whisper-XXL_r245.4_windows.7z`
- `whisper/Whisper-Faster_r186.1_macOS-x86-64.zip`

**Important:** These files are listed in `.gitignore` and will not be committed to the Git repository.

## 2. Updating `whisper_manifest.json` (if necessary)

If the version number, file names, or SHA256 hashes of the updated binaries change, you **must** update the `whisper_manifest.json` file accordingly. This file provides metadata and direct download URLs for the binaries.

Example of `whisper_manifest.json` structure:

```json
{
    "version": "r245.4",
    "artifacts": {
        "windows-x86_64": {
            "url": "https://github.com/guimas-solucoes/tiktok-viral-pro-shared/releases/download/vX.Y.Z/Faster-Whisper-XXL_r245.4_windows.7z",
            "sha256": "NEW_SHA256_HASH_HERE",
            "archive": "7z",
            "entrypoint": "faster-whisper-xxl.exe"
        },
        "linux-x86_64": {
            "url": "https://github.com/guimas-solucoes/tiktok-viral-pro-shared/releases/download/vX.Y.Z/Faster-Whisper-XXL_r245.4_linux.7z",
            "sha256": "NEW_SHA256_HASH_HERE",
            "archive": "7z",
            "entrypoint": "faster-whisper-xxl"
        },
        "macos-x86_64": {
            "url": "https://github.com/guimas-solucoes/tiktok-viral-pro-shared/releases/download/vX.Y.Z/Whisper-Faster_r186.1_macOS-x86-64.zip",
            "sha256": "NEW_SHA256_HASH_HERE",
            "archive": "zip",
            "entrypoint": "whisper-faster"
        }
    }
}
```

**Note:** Update the `url` field to point to the new release tag (e.g., `vX.Y.Z`).

## 3. Creating a New GitHub Release

After updating the local binaries and `whisper_manifest.json` (if needed), follow these steps to create a new GitHub Release:

### Option A: Using the GitHub Web Interface (Recommended for manual uploads)

1. **Commit changes:** Ensure any changes to `whisper_manifest.json` or other relevant files (excluding the binaries themselves) are committed and pushed to your `main` branch.

    ```bash
    git add .
    git commit -m "Prepare for vX.Y.Z release"
    git push origin main
    ```

2. **Create a new Git tag:** Tag the latest commit with a new version number (e.g., `v1.0.1`).

    ```bash
    git tag -a vX.Y.Z -m "Release vX.Y.Z of updated Whisper binaries"
    ```

3. **Push the tag:** Push the newly created tag to your remote repository.

    ```bash
    git push origin vX.Y.Z
    ```

4. **Draft a new release on GitHub:**
    - Go to your repository on GitHub.
    - Click on "Releases" (usually on the right sidebar or under the "Code" tab).
    - Click "Draft a new release" or "Create a new release".
    - Select the new tag you just pushed (e.g., `vX.Y.Z`) from the "Choose a tag" dropdown.
    - Provide a "Release title" (e.g., "Whisper Binaries vX.Y.Z").
    - Write "Release notes" describing the changes or updates.
    - **Attach the binaries:** Drag and drop the updated `Faster-Whisper-XXL_r245.4_linux.7z`, `Faster-Whisper-XXL_r245.4_windows.7z`, and `Whisper-Faster_r186.1_macOS-x86-64.zip` files from your local `whisper/` folder into the "Attach binaries by dropping them here or selecting them" area.
    - Click "Publish release".

### Option B: Using GitHub CLI (`gh cli`)

If you have the GitHub CLI installed and configured, you can automate the release creation and asset upload from your terminal.

1. **Commit changes:** Ensure any changes to `whisper_manifest.json` or other relevant files (excluding the binaries themselves) are committed and pushed to your `main` branch.

    ```bash
    git add .
    git commit -m "Prepare for vX.Y.Z release"
    git push origin main
    ```

2. **Create and publish release with assets:**

    ```bash
    gh release create vX.Y.Z \
      whisper/Faster-Whisper-XXL_r245.4_linux.7z \
      whisper/Faster-Whisper-XXL_r245.4_windows.7z \
      whisper/Whisper-Faster_r186.1_macOS-x86-64.zip \
      --title "Whisper Binaries vX.Y.Z" \
      --notes "Updated pre-compiled Faster-Whisper binaries for various OS."
    ```

    Replace `vX.Y.Z` with your desired new version number.

This `README.md` provides a comprehensive guide for managing future releases of your Whisper binaries.
