# Sample Service

1. Create a new branch on https://gitlab.mercator-ocean.fr/pub/edito-infra/service-playground.
2. Clone the repo locally and switch to your branch:
    - Example:
      `git clone https://gitlab.mercator-ocean.fr/pub/edito-infra/service-playground.git`
      `cd service-playground`
      `git checkout -b <branch-name>`
3. Copy the folder `turbiditymapping-4dvarnet-test` to the repo root.
4. If you rename the folder, follow these rules:
    - The folder name must not start with a number.
    - The branch name, the folder name, and the `name` field in `Chart.yaml` must match exactly.
5. Commit and push your branch:
    - Example: `git add . && git commit -m "Add service" && git push -u origin <branch-name>`
6. The service will be created in the Datalab playground within ~5 minutes after pushing.

Note: Verify the `name` field in `Chart.yaml` is updated if you rename the folder.
