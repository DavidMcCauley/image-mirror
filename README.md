# Public Docker Image Mirror

This repository's purpose is to mirror approved public Docker images from Docker Hub into this organization's public GitHub Container Registry (GHCR).

## Purpose

1.  **Avoid Docker Hub Rate Limiting:** By pulling images once and storing them on GHCR, our CI/CD pipelines can pull from GHCR without being subject to Docker Hub's anonymous user rate limits.
2.  **Centralize Dependencies:** This repository acts as a single source of truth for the approved versions of third-party tools used in our projects.

## Usage

Other projects should pull images from this registry using the following naming convention: `ghcr.io/<your-github-username>/<image-name>:<tag>`

For example, to use Loki, a `docker-compose.yml` file would specify: `image: ghcr.io/your-github-username/grafana-loki:2.8.2`

## How it Works

The workflow in `.github/workflows/mirror.yml` runs on a weekly schedule. It uses a matrix to define the list of images to pull from Docker Hub, retag, and push to GHCR. To add a new image to be mirrored, simply add it to the `matrix.image` list in that file.
