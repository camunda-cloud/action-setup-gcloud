# GitHub Actions to configure Google Cloud connectivity

This GitHub Actions wraps several other GitHub Actions to make it easier to
configure Google Cloud settings and related tools.

In particular:

* It authenticates against Google Cloud Platform and saves the credentials for
  other tools to use them.
* It can automatically login against our Google Container Registry to pull/push
  private Docker images.
* It can optionally install Kubernetes/GKE-related tools, like Kustomize or
  `kubectl`.


## How to use?

Add a new step in your workflow:

```yaml
- name: Configure Google tools
  uses: camunda-cloud/action-setup-gcloud@v1
  with:
    project_id: fun-start-45987
    service_account_key: ${{ secrets.GCP_SERVICE_ACCOUNT_KEY }}
```


### Authenticate Docker

To pull/push private images from our container registries on GCR, configure
Docker to authenticate with:

```yaml
- name: Configure Google tools
  uses: camunda-cloud/action-setup-gcloud@v1
  with:
    # ...
    docker_auth: true
```


### Install Kubernetes/GKE-related tools

To install Kustomize:

```yaml
- name: Configure Google tools
  uses: camunda-cloud/action-setup-gcloud@v1
  with:
    # ...
    kustomize_version: 4.3.0 # or "latest"
```


### Authenticate against GKE

To authenticate against a specific GKE cluster, use:

```yaml
- name: Configure Google tools
  uses: camunda-cloud/action-setup-gcloud@v1
  with:
    # ...

    # The name of the GKE cluster:
    gke_cluster_name: integration-worker-1
    gke_cluster_location: europe-west1 # or a zonal cluster with europe-west1-d
```

This corresponds to the `gcloud container clusters get-credentials $NAME --region $REGION` (or `--zone $ZONE`) `gcloud` command.
