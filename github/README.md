# GitHub Actions Docker images

To update a Docker image for use with GitHub Actions maintained in this repo,
you must:

1. Assuming you have access to upload packages to the Mopidy organization at
   GitHub, you need to create a Personal Access Token (PAT) with the
   `write:packages` and `delete:packages` scopes.

2. Login to the GitHub Container Registry using your local Docker CLI:

    ```
    docker login ghcr.io -u my-github-username --password my-github-packages-pat
    ```

3. Bump the version number in the image directory's `VERSION` file.

4. Do the desired changes to the `Dockerfile`.

5. Run `make build` to build a new Docker image version locally.

6. Test the image locally. Go back to step 4 if the results are not
   satisfactory.

7. Commit all your changes to Git.

8. Run `make release` to tag a new release in Git and Docker, to push the
   source changes to the GitHub repo, and the new Docker image to GitHub Container Registry.
