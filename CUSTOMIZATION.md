# Sub2API custom fork workflow

This fork keeps two important branches:

- `main`: tracks the official fork baseline.
- `custom-lmh`: the deployable custom branch for local modifications.

## Docker image

Every push to `custom-lmh` builds and publishes:

```text
ghcr.io/lur1n77777/sub2api:custom
ghcr.io/lur1n77777/sub2api:custom-<commit-sha>
```

Use `:custom` in the server `docker-compose.yml` when you are ready to deploy custom builds.

## Upstream updates

The `Sync upstream into custom branch` workflow runs daily and can also be triggered manually. It merges official upstream `Wei-Shaw/sub2api:main` into a temporary branch named `sync/upstream-main`, then opens or updates a PR into `custom-lmh`.

This is intentionally PR-based instead of silent auto-merge, so official changes can be reviewed before they affect your deployed custom image.

## Recommended customization process

1. Make changes only on `custom-lmh`.
2. Keep changes small and config-gated when possible.
3. Let the sync workflow open PRs for upstream updates.
4. Merge the sync PR after review.
5. Deploy the new `ghcr.io/lur1n77777/sub2api:custom` image.