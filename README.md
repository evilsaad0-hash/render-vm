# EVILSAAD JUPYTER

Custom-branded JupyterLab container for Render.

## Deploy on Render

1. Upload this folder to a GitHub repository.
2. In Render, choose **New > Blueprint** and connect the repository.
3. Render reads `render.yaml` and creates the Docker web service.
4. In the service's Environment settings, ensure `JUPYTER_TOKEN` is set to a long, private secret. The Blueprint requests a generated value; do not share it.
5. Open the service URL and authenticate with the token.

## Local Docker

```bash
docker build -t evilsaad-jupyter .
docker run --rm -p 10000:10000 \
  -e JUPYTER_TOKEN='replace-with-a-long-random-secret' \
  evilsaad-jupyter
```

Open `http://localhost:10000`.

## Included packages

JupyterLab, ipykernel, NumPy, pandas, Matplotlib, seaborn, requests, BeautifulSoup, Pillow, SciPy and scikit-learn.

## Storage warning

The default Render free service does not provide durable local storage. Notebook files may be lost when the instance is replaced. Attach a persistent disk on a plan that supports it and mount it at `/home/jovyan/work` if persistence is required.

## Security

- `JUPYTER_TOKEN` is mandatory; the server refuses to start without it.
- Do not commit secrets into GitHub.
- This project is intended for a trusted single user. It does not implement user registration, per-user isolation, or a public multi-tenant VPS service.
