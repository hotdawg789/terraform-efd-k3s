terraform efd-k3s "top level" deployment
===

[![Build Status](https://travis-ci.org/lsst-sqre/terraform-efd-k3s.png)](https://travis-ci.org/lsst-sqre/terraform-efd-k3s)

Deploys an `efd` instance on top of a `k3s` cluster. At this moment the `k3s` cluster is created following
the instructions in [SQR-31](https://sqr-031.lsst.io).

Usage
---

This package is intended to be used as a "top level" deployment, rather than as
a general purpose module, and thus declares provider configuration that
may be inappropriate in a module.

`terragrunt` configuration example:

```terraform
terragrunt = {
  terraform {
    source = "git::https://github.com/lsst-sqre/terraform-efd-k3s.git//?ref=master"
  }
}
```

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| aws\_zone\_id | route53 Hosted Zone ID to manage DNS records in. | string | n/a | yes |
| brokers\_disk\_size | Disk size for the cp-kafka brokers. | string | `"15Gi"` | no |
| deploy\_name | Name of deployment. | string | `"efd"` | no |
| dns\_enable | create route53 dns records. | string | `"false"` | no |
| dns\_overwrite | overwrite pre-existing DNS records | string | `"false"` | no |
| domain\_name | DNS domain name to use when creating route53 records. | string | n/a | yes |
| enable\_telegraf\_daemonset | If true Telegraf client will run on all nodes. Set false for k3s single node deployment. | string | `"true"` | no |
| env\_name | Name of deployment environment. | string | n/a | yes |
| github\_token | GitHub personal access token for authenticating to the GitHub API | string | n/a | yes |
| github\_user | GitHub username for authenticating to the GitHub API. | string | n/a | yes |
| grafana\_admin\_pass | grafana admin account passphrase. | string | n/a | yes |
| grafana\_admin\_user | grafana admin account name. | string | `"admin"` | no |
| grafana\_oauth\_client\_id | github oauth Client ID for grafana | string | n/a | yes |
| grafana\_oauth\_client\_secret | github oauth Client Secret for grafana. | string | n/a | yes |
| grafana\_oauth\_team\_ids | github team id (integer value treated as string) | string | n/a | yes |
| influxdb\_admin\_pass | influxdb admin account passphrase. | string | n/a | yes |
| influxdb\_admin\_user | influxdb admin account name. | string | `"admin"` | no |
| influxdb\_telegraf\_pass | InfluxDB password for the telegraf user. | string | n/a | yes |
| kafka\_loadbalancers | Number of Kafka loadbalancers. Must be less or equal to the number of Kafka brokers. Set to 1 for k3s single node deployment. | string | `"3"` | no |
| kubeconfig\_filename | kubeconfig file to configure kubernetes/helm providers | string | n/a | yes |
| prometheus\_oauth\_client\_id | github oauth client id | string | n/a | yes |
| prometheus\_oauth\_client\_secret | github oauth client secret | string | n/a | yes |
| prometheus\_oauth\_github\_org | limit access to prometheus dashboard to members of this org | string | n/a | yes |
| storage\_class | Storage class to be used for all persistent disks. For a deployment on k3s use 'local-path'. | string | `"pd-ssd"` | no |
| tls\_crt\_path | wildcard tls certificate. | string | n/a | yes |
| tls\_key\_path | wildcard tls private key. | string | n/a | yes |
| zookeeper\_data\_dir\_size | Size for Data dir, where ZooKeeper will store the in-memory database snapshots. | string | `"15Gi"` | no |
| zookeeper\_log\_dir\_size | Size for data log dir, which is a dedicated log device to be used, and helps avoid competition between logging and snaphots. | string | `"15Gi"` | no |

## Outputs

| Name | Description |
|------|-------------|
| confluent\_lb\_ips |  |
| grafana\_fqdn |  |
| influxdb\_fqdn |  |
| nginx\_ingress\_ip |  |
| prometheus\_fqdn |  |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

`helm`
---

Note that the `helm` provider is used, which requires an initialized `helm`
repo configuration.

`pre-commit` hooks
---

```bash
go get github.com/segmentio/terraform-docs
pip install --user pre-commit
pre-commit install

# manual run
pre-commit run -a
```

See Also
---

* [`terraform`](https://www.terraform.io/)
* [`terragrunt`](https://github.com/gruntwork-io/terragrunt)
* [`terraform-docs`](https://github.com/segmentio/terraform-docs)
* [`helm`](https://docs.helm.sh/)
* [`pre-commit`](https://github.com/pre-commit/pre-commit)
* [`pre-commit-terraform`](https://github.com/antonbabenko/pre-commit-terraform)
