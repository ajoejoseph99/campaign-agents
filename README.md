## 1. Enable Required APIs
Cloud Run deployments from source require Artifact Registry (to store the container), Cloud Build (to build it), and Cloud Run itself. Enable them all at once:
```
gcloud services enable artifactregistry.googleapis.com cloudbuild.googleapis.com run.googleapis.com
```

## 2. Set Default Region
```
gcloud config set run/region us-central1
```

## 3. Grant Necessary IAM Permissions
For a fresh project, the default Compute Engine service account needs permission to push your source code to the staging storage bucket during the build phase.
```
gcloud projects add-iam-policy-binding ai-fdp-rset \
  --member="serviceAccount:554310971774-compute@developer.gserviceaccount.com" \
  --role="roles/storage.admin"
```

## 4. The Clean Deployment Command
(Remember to replace YOUR_API_KEY before running it!).

Get your api key from https://aistudio.google.com/api-keys
```
gcloud run deploy marketing-agents --source . --set-env-vars="GEMINI_API_KEY=YOUR_API_KEY" --allow-unauthenticated
```
