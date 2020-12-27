# GitHub Actions Docker images

To update a Docker image for use with CircleCI maintained in this repo, you
must:

1. Assuming you have access to upload packages to the Mopidy organization at
   GitHub, you need to create a Personal Access Token (PAT) with the
   `write:packages` and `delete:packages` scopes.

1. Login to the GitHub Container Registry using your local Docker CLI:

    ```
    docker login ghcr.io -u my-github-username --password my-github-packages-pat
    ```

2. Bump the version number in the image directory's `VERSION` file.

3. Do the desired changes to the `Dockerfile`.

4. Run `make build` to build a new Docker image version locally.

5. Test the image locally. Go back to step 3 if the results are not
   satisfactory.

6. Commit all your changes to Git.

7. Run `make release` to tag a new release in Git and Docker, to push the
   source changes to the GitHub repo, and the new Docker image to GitHub Container Registry.
