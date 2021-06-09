# nac-sandbox-cluster

An experimental Kubernetes cluster for some NAC-owned deployments

## Documentation

See <https://codeforamerica.github.io/nac-sandbox-cluster/>

## Repository contents

- `.github/workflows/publish-holobranches.yml`: GitHub Actions workflow that handles updating projected holobranches on push to the `main` branch
- `.holo/`: Declares `k8s-manifests` and `docs-site` holobranches
    - `.holo/branches/docs-site/`: Rendered MkDocs website that powers this repository's GitHub Pages website
    - `.holo/branches/k8s-manifests/`: Rendered Kubernetes manifests declaring entire cluster
    - `.holo/branches/k8s-manifests-github/`: `k8s-manifests` holobranch with civic-cloud GitHub Actions workflows added
- `docs/`: Documentation content to overlay civic-cloud docs with
- `mkdocs.site.yml`: Site-specific overrides for MkDocs configuration
- `grafana/release-values.yaml`: Values overrides for Grafana Helm chart [included in upstream civic-cloud blueprint](https://github.com/CodeForPhilly/civic-cloud/blob/k8s/blueprint/common/grafana/release-values.yaml)
- **The rest**: loose manifests and Helm charts for local cluster content

## Metrics

Grafana is available at <https://metrics.sandbox.k8s.brigade.cloud>

- Deployed from civic-cloud template
- See `grafana/grafana-initial-admin` secret for login

## References

- <https://jarvuslabs.github.io/library/kubernetes/shared-clusters/create-cluster/>
- <http://civic-cloud.phl.io/>
