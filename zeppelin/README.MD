# Apache Zeppelin

This initialization action installs the latest version of [Apache Zeppelin](https://zeppelin.apache.org/) on a master node within a [Google Cloud Dataproc](https://cloud.google.com/dataproc) cluster.

## Using this initialization action
You can use this initialization action to create a new Dataproc cluster with Apache Zeppelin installed:

1. Use the `gcloud` command to create a new cluster with this initialization action. The following command will create a new cluster named `<CLUSTER_NAME>`.

    ```bash
    gcloud dataproc clusters create <CLUSTER_NAME> \
      --initialization-actions gs://dataproc-initialization-actions/zeppelin/zeppelin.sh
    ```
1. Once the cluster has been created, Zeppelin is configured to run on port `8080` on the master node in a Dataproc cluster. To connect to the Apache Zeppelin web interface, you will need to create an SSH tunnel and use a SOCKS 5 Proxy as described in the [dataproc web interfaces](https://cloud.google.com/dataproc/cluster-web-interfaces) documentation.

### Options

This option can be provided as a metadata key using `--metadata`.

* `zeppelin-port`=<integer>: Port on which the Zeppelin server runs

For example:

```bash
gcloud dataproc clusters create <CLUSTER_NAME> \
  --initialization-actions gs://dataproc-initialization-actions/zeppelin/zeppelin.sh \
  --metadata zeppelin-port=8081
```

## Important notes
* This installs Zeppelin 0.5.6 in Dataproc 1.0, Zeppelin 0.6.1 in Dataproc 1.1, and Zeppelin 0.7 in Dataproc 1.2.
* It configures the BigQuery interpreter in 0.6.1+.
* It installs `matplotlib`. More information about Zeppelin/matplotlib integration [here](https://zeppelin.apache.org/docs/latest/interpreter/python.html#matplotlib-integration).
* By default it only install Rs graphing libraries that ship with Debian 8 (ggplot2, knitr, and googlevis).
  * To install the other required R libraries (mplot and rCharts), uncomment lines after "Uncomment here" in zeppelin.sh.
  * There are still some issues with examples in the R Tutorial (under investation).
* The Hive interpreter in missing in Dataproc 1.1.
