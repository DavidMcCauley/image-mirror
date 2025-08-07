# Contributing to Public Docker Image Mirror

Thank you for your interest in contributing! This project helps centralize our public Docker image dependencies and avoid rate-limiting from external registries.

## How to Add a New Image

Adding a new public image to be mirrored is simple:

1.  **Fork the repository.**
2.  **Edit `images.txt`:** Add the full name and tag of the public image you wish to mirror to a new line in the `images.txt` file.
    ```
    # Example:
    redis:7.0
    ```
3.  **Submit a Pull Request:** Open a pull request with your change. The CI workflow will automatically run to validate that the image can be pulled.

Once the pull request is merged, the new image will be mirrored to our GitHub Container Registry on the next scheduled run.
