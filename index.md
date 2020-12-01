## CDAB Helm repo

Helm repo, how to use

### Update the helm index

Update the index if you add a new package, or update existing packages

1. Pack the helm chart

        $ helm package /path/to/my-helm-chart

2. Move the package to the root of the helm repo (This git repo)

        $ mv my-helm-chart-1.2.3.tgz /path/to/helm-repo

3. Update the helm index.yaml file

        $ cd /path/to/helm-repo
        $ helm repo index . --merge index.yaml --url https://charts.cdab.eu

4. Verify index.yaml looks correct

5. Commit and push changes in this repo