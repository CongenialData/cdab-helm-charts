## CDAB Helm charts

You can add this repository to you local helm configuration like this:

```console
$ helm repo add {{ site.repo_name }} {{ site.url }}
$ helm repo update
```

### Update the helm index

Update the index if you add a new package, or update existing packages

1. Pack the helm chart

    ```console
    $ helm package /path/to/my-helm-chart
    ```

2. Move the package to the root of the helm repo (This git repo)
    ```console
    $ mv my-helm-chart-1.2.3.tgz /path/to/helm-repo
    ```

3. Update the helm index.yaml file

    ```console
    $ cd /path/to/helm-repo
    $ helm repo index . --merge index.yaml --url https://charts.cdab.eu
    ```

4. Verify index.yaml looks correct

5. Commit and push changes in this repo