# szurubooru

![Version: 1.0.1](https://img.shields.io/badge/Version-1.0.1-informational?style=flat-square) ![AppVersion: v2.5.0](https://img.shields.io/badge/AppVersion-v2.5.0-informational?style=flat-square)

Szurubooru is an image board engine inspired by services such as Danbooru, Gelbooru and Moebooru
dedicated for small and medium communities.

**This chart is not maintained by the upstream project and any issues with the chart should be raised [here](https://github.com/toboshii/charts/issues/new/choose)**

## Source Code

* <https://github.com/rr-/szurubooru>

## Requirements

Kubernetes: `>=1.16.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| https://charts.bitnami.com/bitnami | postgresql | 10.5.3 |
| https://library-charts.k8s-at-home.com | common | 4.0.0 |

## TL;DR

```console
helm repo add toboshii https://toboshii.github.io/charts/
helm repo update
helm install szurubooru toboshii/szurubooru
```

## Installing the Chart

To install the chart with the release name `szurubooru`

```console
helm install szurubooru toboshii/szurubooru
```

## Uninstalling the Chart

To uninstall the `szurubooru` deployment

```console
helm uninstall szurubooru
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install szurubooru \
  --set env.TZ="America/New York" \
    toboshii/szurubooru
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install szurubooru toboshii/szurubooru -f values.yaml
```

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| additionalContainers.server.env | list | See below (only deviations from the default settings are specified) | environment variables. See [image docs](https://github.com/rr-/szurubooru/blob/master/docker-compose.yml) for more details. |
| additionalContainers.server.env[0] | object | `{"name":"TZ","value":"UTC"}` | Set the container timezone |
| additionalContainers.server.env[1] | object | `{"name":"POSTGRES_HOST","value":"{{ .Release.Name }}-postgresql"}` | Postgres database hostname |
| additionalContainers.server.env[2] | object | `{"name":"POSTGRES_PORT","value":5432}` | Postgres custom port (empty = default port) |
| additionalContainers.server.env[3] | object | `{"name":"POSTGRES_USER","value":"szurubooru"}` | Postgres database username |
| additionalContainers.server.env[4] | object | `{"name":"POSTGRES_PASSWORD","value":"szurubooru"}` | Postgres database password |
| additionalContainers.server.env[5] | object | `{"name":"POSTGRES_DB","value":"szurubooru"}` | Postgres database name |
| additionalContainers.server.env[6] | object | `{"name":"LOG_SQL","value":0}` | Set to 1 to enable verbose SQL logs |
| additionalContainers.server.image | string | `"szurubooru/server:2.5-edge"` |  |
| additionalContainers.server.imagePullPolicy | string | `"IfNotPresent"` |  |
| additionalContainers.server.name | string | `"server"` |  |
| additionalContainers.server.volumeMounts | list | `[]` |  |
| env | object | See below (only deviations from the default settings are specified) | environment variables. See [image docs](https://github.com/rr-/szurubooru/blob/master/docker-compose.yml) for more details. |
| env.BACKEND_HOST | string | `"{{ .Release.Name }}-server"` | Set the backend host |
| env.BASE_URL | string | `"https://example.com"` | Set the base URL |
| env.TZ | string | `"UTC"` | Set the container timezone |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"szurubooru/client"` | image repository |
| image.tag | string | `"2.5-edge"` | image tag |
| ingress.main | object | See values.yaml | Enable and configure ingress settings for the chart under this key. |
| persistence | object | See values.yaml | Configure persistence settings for the chart under this key. |
| postgresql | object | See values.yaml | Enable and configure postgresql database subchart under this key.    For more options see [postgresql chart documentation](https://github.com/bitnami/charts/tree/master/bitnami/postgresql) |
| service | object | See values.yaml | Configures service settings for the chart. |
| szurubooru | object | See below | Configures Szurubooru settings. See [app docs](https://github.com/rr-/szurubooru/blob/master/server/config.yaml.dist) for more details. |
| szurubooru.domain | string | `"https://example.com"` | Full url to the homepage of this szurubooru site, with no trailing slash |
| szurubooru.name | string | `"szurubooru"` | Shown in the website title and on the front page |
| szurubooru.secret | string | `"change"` | Used to salt the users' password hashes and generate filenames for static content |

## Support

- See the [Docs](https://docs.k8s-at-home.com/our-helm-charts/getting-started/)
- Open an [issue](https://github.com/toboshii/charts/issues/new/choose)
- Join our [Discord](https://discord.gg/sTMX7Vh) community

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.5.0](https://github.com/norwoodj/helm-docs/releases/v1.5.0)

