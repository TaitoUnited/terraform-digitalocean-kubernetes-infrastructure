# Kubernetes infrastructure for Digital Ocean

Kubernetes infrastructure module designed to get you up and running in no time. Provides all the necessary components for running your projects: Kubernetes, NGINX ingress, cert-manager, container registry, databases, database proxies, networking, monitoring, and permissions. Use it either as a module, or as an example for your own customized infrastructure.

This module is used by [infrastructure templates](https://taitounited.github.io/taito-cli/templates#infrastructure-templates) of [Taito CLI](https://taitounited.github.io/taito-cli/). See the [do template](https://github.com/TaitoUnited/taito-templates/tree/master/infrastructure/do/terraform) as an example on how to use this module.

```
kubernetes:
  name: zone1-common-kube
  context: zone1
  version: 1.16.2-do.1
  nodePools:
    - name: pool-1
      machineType: s-2vcpu-2gb
      diskSizeGb: 100
      minNodeCount: 2
      maxNodeCount: 2
  ingressNginxControllers:
    - class: nginx
      replicas: 2

postgresClusters:
  - name: zone1-common-postgres
    version: 11
    tier: db-s-1vcpu-1gb
    nodeCount: 1
    # TODO: support for db users
    users:
      - username: john.doe
        read:
          - my-project-prod
        write:
          - another-project-prod

mysqlClusters:
  - name: ${taito_zone}-common-mysql
    tier: db-s-1vcpu-1gb
    nodeCount: 1
    # TODO: support for db users
    users:
      - username: john.doe
        read:
          - my-project-prod
        write:
          - another-project-prod
```
