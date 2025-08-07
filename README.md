# Public Docker Image Mirror

This repository's purpose is to mirror approved public Docker images from registries like Docker Hub and GCR into this organization's public GitHub Container Registry (GHCR).

## Purpose

1.  **Avoid Rate Limiting:** By pulling images once and storing them on GHCR, our CI/CD pipelines can pull from GHCR without being subject to external registry rate limits.
2.  **Centralize Dependencies:** This repository acts as a single source of truth for the approved versions of third-party tools used in our projects.
3.  **Improve Reliability:** It protects our workflows from outages or changes in external registries.

## How it Works

A single, consolidated GitHub Actions workflow in `.github/workflows/mirror.yml` orchestrates the entire process:

1.  **Read Image List:** The workflow reads a list of images from the `images.txt` file in the root of the repository. This file is the single source of truth.
2.  **Mirror Images:** On a weekly schedule (or when run manually), the workflow pulls each image, re-tags it for GHCR, and pushes the new version. It's smart enough to skip mirroring if the latest version already exists on GHCR.
3.  **Cleanup Old Images:** After a successful mirror run, a cleanup job automatically deletes all but the single most recent version of each mirrored package. This keeps our storage usage low.

## How to Use Mirrored Images

Other projects should pull images from this registry using the following naming convention: `ghcr.io/<your-github-owner>/<image-name-with-hyphens>:<tag>`

For example, to use Loki, a `docker-compose.yml` file would specify: `image: ghcr.io/your-github-owner/grafana-loki:2.8.2`

## How to Contribute

To add a new image to be mirrored, please see our [**Contributing Guidelines**](CONTRIBUTING.md).
