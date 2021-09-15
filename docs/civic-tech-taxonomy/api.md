# API

## Deployment

1. Merge or push new commits into the `master` branch in the [`civic-tech-taxonomy` repository](https://github.com/codeforamerica/civic-tech-taxonomy)
1. After pushing to the `master` branch, you should see the `publish-api-server` GitHub Action running or already complete [under the Actions tab](https://github.com/codeforamerica/civic-tech-taxonomy/actions/workflows/publish-api-server.yml)
1. Once the action finishes, you should be able to confirm that a new tag has been push for [the `api-server` container image](https://github.com/codeforamerica/civic-tech-taxonomy/pkgs/container/civic-tech-taxonomy%2Fapi-server) matching the SHA of your latest commit to the `master` branch that it was built from
1. In the [`nac-sandbox-cluster` repository](https://github.com/codeforamerica/nac-sandbox-cluster), edit the file [`civic-tech-taxonomy/api-server.yaml`](https://github.com/codeforamerica/nac-sandbox-cluster/blob/main/civic-tech-taxonomy/api-server.yaml) which declares the deployment for the `api-server` instance hosted on the cluster
    1. Find the line specifying the container image path+tag:

        ```yaml
        image: ghcr.io/codeforamerica/civic-tech-taxonomy/api-server:abcdef1
        ```

    1. Change the tag portion of the line to match the hash for the one that was just built
    1. Commit your change directly to the `main` branch on the cluster repository if you have access, otherwise open a pull request and ask a cluster administrator to merge it for you. **No change will actually get applied to the cluster at this point**
1. After the `image` value has been updated in the `main` branch in the `nac-sandbox-cluster` repository, that repository's [`prepare-k8s-manifests` action](https://github.com/codeforamerica/nac-sandbox-cluster/actions/workflows/prepare-k8s-manifests.yml) will prepare an automated PR for deploying the change to the cluster. Review that PR and ask a cluster administrator to merge it for you.
1. Once the deploy PR is merged, the new version should be online within a few minutes.
