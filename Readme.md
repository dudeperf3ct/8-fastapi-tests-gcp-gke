# Sentiment Classification

Exposed endpoint : http://34.66.115.66:8000/

In this project, we will deploy a sentiment analyser model using fastapi on GCP using GKE.

- Containerizing different components of projects
- Writing tests and testing individual modules using `pytest`
- Using [trunk](https://docs.trunk.io/) for automatic code checking, formatting and liniting
- Deploying application on GKE

## Run

### Locally

- Sentiment Model

```bash
cd sentiment
docker build -t sentiment -f Dockerfile.t .
cd ..
docker run --rm -it -v $(pwd):/app sentiment bash
python3 sentiment/model.py
pytest tests/test_sentiment_model.py
```

- FastAPI

> Note: To run `pytest` replace `requirements-fastapi.txt` with `requirements-dev.txt` in `Dockerfile`

```bash
docker build -t sentiment -f Dockerfile.fastapi .
docker run --rm -it -v $(pwd):/app -p 8000:8000 sentiment bash
uvicorn main:app --host=0.0.0.0
pytest --cov tests/
```

- GKE

Deploy the application on Google Kubernetes Engine (GKE).

Guide: https://cloud.google.com/kubernetes-engine/docs/how-to/automated-deployment

Expose port of 8000 after deploy under `Workloads > ACTIONS > Expose` in Kubernetes Engine 

Setup up automatic deploy using Cloud Build and Github under `Workloads > ACTIONS > Automated deployment`. 

## Additional Exercise

- Deploy this application using gcloud cli