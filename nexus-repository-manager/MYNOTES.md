# Notes

Helm chart is hosted from root directory with GitHub pages. The index.yaml points into `docs/`.

Add the repo to local helm with:

`helm repo add jimsnab-charts https://jimsnab.github.io/nxrm3-helm-repository`

Verify you can find the modified chart with:

`helm search repo nexus-repository-manager`

To make a code change:

1. Modify the template
1. Do various testing steps like `helm template nexus-repository-manager` and examine output, or `helm install --dryrun`.
1. Package from the root of the clone with `helm package nexus-repository-manager/ --destination docs`
1. Regenerate the index from the root of the clone with `helm repo index --url https://jimsnab.github.io/nxrm3-helm-repository/ .`
1. Push changes to github main branch. It might be necessary to remove the read only lock.

It's a good idea to update the version in `Chart.yaml` when you make a change, and then explicitly
request that version.

Example deploy with Terraform:

```
resource "helm_release" "sonatype_release" {
  repository = "https://jimsnab.github.io/nxrm3-helm-repository/"
  chart = "nexus-repository-manager"
  name  = "sonatype"
  version = "47.0.1"

  ...

}
```
