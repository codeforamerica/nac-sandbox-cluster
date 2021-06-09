# MySQL

An instance of MySQL is hosted to serve a working copy of taxonomy data as loaded by <https://github.com/codeforamerica/civic-tech-taxonomy/tree/master/tools/mysql-loader>

## Using portforwarder service account

1. Download the `civic-tech-taxonomy-portforwarder.yaml` from a teammate into your `~/.kube` directory

    Or, initially using the root `KUBECONFIG` for the entire cluster, generate a narrowly-scoped `KUBECONFIG` file for the `civic-tech-taxonomy/portforwarder` service account:

    ```bash
    sudo hab pkg install jarvus/mkkubeconfig
    hab pkg exec jarvus/mkkubeconfig mkkubeconfig civic-tech-taxonomy portforwarder > ~/.kube/civic-tech-taxonomy-portforwarder.yaml
    ```

2. Activate the downloaded `KUBECONFIG` in your current terminal session:

    ```bash
    export KUBECONFIG=~/.kube/civic-tech-taxonomy-portforwarder.yaml
    ```

3. Get the name of the currently running pods and store them in shell variables:

    ```bash
    MYSQL_POD=$(kubectl get pod -l service=mysql -o jsonpath='{.items[0].metadata.name}')
    ```

### Forward PostgreSQL port

```bash
kubectl port-forward "pods/$(kubectl get pod -l service=mysql -o jsonpath='{.items[0].metadata.name}')" 3306:3306
```

!!! tip "Database logins"
    Default database username is `root` and password is currently set in `civic-tech-taxonomy/mysql.yaml`
