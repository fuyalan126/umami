# Cyberserval Umami Deployment

This deployment uses the custom image built from this fork:

```text
ghcr.io/fuyalan126/umami:latest
```

## Build image

Push changes to `master`, or run the `Build custom Umami image` workflow manually in GitHub Actions.

The workflow publishes:

```text
ghcr.io/fuyalan126/umami:latest
ghcr.io/fuyalan126/umami:master
ghcr.io/fuyalan126/umami:sha-<commit>
```

## Deploy on server

On `prod-umami`:

```bash
cd ~/umami
sudo docker compose pull umami
sudo docker compose up -d
sudo docker compose ps
```

If the GHCR package is private, log in first with a GitHub token that has `read:packages`:

```bash
echo "YOUR_GITHUB_TOKEN" | sudo docker login ghcr.io -u fuyalan126 --password-stdin
```

Alternatively, make the package public in GitHub Packages so the server can pull it without authentication.

## Roll back

Set the `umami` image back to the previous official image or a previous `sha-<commit>` image, then run:

```bash
sudo docker compose pull umami
sudo docker compose up -d
```
