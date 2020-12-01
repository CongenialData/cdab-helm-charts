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

## Charts

{% for helm_chart in site.data.index.entries %}
{% assign title = helm_chart[0] | capitalize %}
{% assign all_charts = helm_chart[1] | sort: 'created' | reverse %}
{% assign latest_chart = all_charts[0] %}

<h3>
  {% if latest_chart.icon %}
  <img src="{{ latest_chart.icon }}" style="height:1.2em;vertical-align: text-top;" />
  {% endif %}
  {{ title }}
</h3>

[Home]({{ latest_chart.home }}) \| [Source]({{ latest_chart.sources[0] }})

{{ latest_chart.description }}

```console
$ helm install myrelease {{ site.repo_name }}/{{ latest_chart.name }} --version {{ latest_chart.version }}
```

| Chart Version | App Version | Date |
|---------------|-------------|------|
{% for chart in all_charts -%}
{% unless chart.version contains "-" -%}
| [{{ chart.name }}-{{ chart.version }}]({{ chart.urls[0] }}) | {{ chart.appVersion }} | {{ chart.created | date_to_rfc822 }} |
{% endunless -%}
{% endfor -%}

{% endfor %}