# Development workflow: home laptop and university lab PC

## Source of truth

GitHub is the source of truth for project code, configuration, documentation, and small reproducible scripts. Keep the 21 GB university dataset on the lab PC (and any institution-approved storage only). Never add dataset files, derived point clouds, labels, checkpoints, or private credentials to Git.

## Home laptop

1. Clone the project repository.
2. Create/edit Python source, tests, YAML configs, documentation, and small synthetic test fixtures.
3. Run CPU-only unit tests and static checks where possible.
4. Review `git status` and `git diff`.
5. Commit and push.

The home laptop does not need the university dataset or a CUDA installation for code authoring. If it has a compatible NVIDIA GPU, a separate local environment can be considered after checking its hardware.

## Lab PC

1. Pull the latest project changes.
2. Activate the already-working lab Conda environment.
3. Keep the modified VoD dataset at its existing lab storage path.
4. Run data inspection and a small smoke test first.
5. Train and validate on the lab GPU.
6. Save logs/checkpoints outside the Git repository; commit only scripts, configs, and concise result summaries that are allowed to be shared.

## Before switching machines

On the machine where you worked:

```bash
git status
git add README.md .gitignore docs src configs scripts tests
git diff --cached
git commit -m "Describe the work"
git push
```

On the other machine:

```bash
git pull --ff-only
git status
```

If Git reports local changes or a conflict, stop and inspect before using reset, clean, or force-push. Never use `git push --force` as a routine sync method.

## Dataset and permission

The assignment says the modified VoD split supplied by the supervisor should be used, and the official dataset authors' permission is still required. Confirm/retain the required permission before research use. The dataset must not be uploaded to this repository. Ask the supervisor before making project code or derived results public because the assignment states that rights to collected project data and duties pass to the chair, which is authorized to use results and software.

## Reproducibility

For every experiment, record:
- Git commit hash
- Dataset version/path identifier (not private download credentials)
- Split definition and random seed
- Python, PyTorch, CUDA runtime, NVIDIA driver, spconv and OpenPCDet versions
- GPU model
- Configuration and command
- Metrics, runtime, and output location

Do not tune hyperparameters on the test split. The assignment requires three random seeds and validation-only hyperparameter selection.
