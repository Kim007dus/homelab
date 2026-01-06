```shell
k get all -n auth
NAME                       READY   STATUS    RESTARTS   AGE
pod/dex-6c99968d84-zbgg7   1/1     Running   0          18m

NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
service/dex   ClusterIP   10.43.240.18   <none>        5556/TCP   18m

NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/dex   1/1     1            1           18m

NAME                             DESIRED   CURRENT   READY   AGE
replicaset.apps/dex-6c99968d84   1         1         1       18m
k get all -n cert-manager
NAME                                           READY   STATUS        RESTARTS   AGE
pod/cert-manager-5f864bbfd-56lmx               1/1     Running       0          11m
pod/cert-manager-5f864bbfd-pdcdm               1/1     Terminating   0          18m
pod/cert-manager-cainjector-589dc747b5-cpk4f   1/1     Running       0          18m
pod/cert-manager-webhook-5987c7ff58-jn8c2      1/1     Running       0          11m
pod/cert-manager-webhook-5987c7ff58-psgbx      1/1     Terminating   0          18m

NAME                              TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)            AGE
service/cert-manager              ClusterIP   10.43.179.103   <none>        9402/TCP           19m
service/cert-manager-cainjector   ClusterIP   10.43.30.111    <none>        9402/TCP           19m
service/cert-manager-webhook      ClusterIP   10.43.197.42    <none>        443/TCP,9402/TCP   19m

NAME                                      READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/cert-manager              1/1     1            1           18m
deployment.apps/cert-manager-cainjector   1/1     1            1           18m
deployment.apps/cert-manager-webhook      1/1     1            1           18m

NAME                                                 DESIRED   CURRENT   READY   AGE
replicaset.apps/cert-manager-5f864bbfd               1         1         1       18m
replicaset.apps/cert-manager-cainjector-589dc747b5   1         1         1       18m
replicaset.apps/cert-manager-webhook-5987c7ff58      1         1         1       18m
```

```shell
k get all -n istio-system
NAME                                        READY   STATUS    RESTARTS   AGE
pod/cluster-local-gateway-8f84bb6fb-8b64g   1/1     Running   0          19m
pod/istio-ingressgateway-68d8b7b94f-t2zbz   1/1     Running   0          19m
pod/istiod-746c8788fd-g2f82                 1/1     Running   0          19m

NAME                            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                                 AGE
service/cluster-local-gateway   ClusterIP   10.43.4.116     <none>        15020/TCP,80/TCP                        19m
service/istio-ingressgateway    ClusterIP   10.43.92.36     <none>        15021/TCP,80/TCP,443/TCP                19m
service/istiod                  ClusterIP   10.43.71.148    <none>        15010/TCP,15012/TCP,443/TCP,15014/TCP   19m
service/knative-local-gateway   ClusterIP   10.43.151.158   <none>        80/TCP,443/TCP                          19m

NAME                                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/cluster-local-gateway   1/1     1            1           19m
deployment.apps/istio-ingressgateway    1/1     1            1           19m
deployment.apps/istiod                  1/1     1            1           19m

NAME                                              DESIRED   CURRENT   READY   AGE
replicaset.apps/cluster-local-gateway-8f84bb6fb   1         1         1       19m
replicaset.apps/istio-ingressgateway-68d8b7b94f   1         1         1       19m
replicaset.apps/istiod-746c8788fd                 1         1         1       19m

NAME                                                        REFERENCE                          TARGETS       MINPODS   MAXPODS   REPLICAS   AGE
horizontalpodautoscaler.autoscaling/cluster-local-gateway   Deployment/cluster-local-gateway   cpu: 7%/80%   1         5         1          18m
horizontalpodautoscaler.autoscaling/istio-ingressgateway    Deployment/istio-ingressgateway    cpu: 4%/80%   1         5         1          18m
horizontalpodautoscaler.autoscaling/istiod                  Deployment/istiod                  cpu: 2%/80%   1         5         1          18m
```

```shell
k get all -n knative-serving
NAME                                        READY   STATUS    RESTARTS   AGE
pod/activator-67ffb64667-vxk9m              2/2     Running   0          18m
pod/autoscaler-7494b9b9cf-5mnvz             2/2     Running   0          18m
pod/controller-76858fd78b-mjtfn             2/2     Running   0          18m
pod/net-istio-controller-5c59fd6669-pvqqc   2/2     Running   0          18m
pod/net-istio-webhook-595d94fbb5-m7hst      2/2     Running   0          18m
pod/webhook-59c4ddb9d-b7vkl                 2/2     Running   0          18m

NAME                                 TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                                   AGE
service/activator-service            ClusterIP   10.43.216.125   <none>        9090/TCP,8008/TCP,80/TCP,81/TCP,443/TCP   20m
service/autoscaler                   ClusterIP   10.43.16.251    <none>        9090/TCP,8008/TCP,8080/TCP                20m
service/autoscaler-bucket-00-of-01   ClusterIP   10.43.182.18    <none>        8080/TCP                                  17m
service/controller                   ClusterIP   10.43.231.254   <none>        9090/TCP,8008/TCP                         20m
service/net-istio-webhook            ClusterIP   10.43.219.132   <none>        9090/TCP,8008/TCP,443/TCP                 20m
service/webhook                      ClusterIP   10.43.31.35     <none>        9090/TCP,8008/TCP,443/TCP                 20m

NAME                                   READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/activator              1/1     1            1           19m
deployment.apps/autoscaler             1/1     1            1           19m
deployment.apps/controller             1/1     1            1           19m
deployment.apps/net-istio-controller   1/1     1            1           19m
deployment.apps/net-istio-webhook      1/1     1            1           19m
deployment.apps/webhook                1/1     1            1           19m

NAME                                              DESIRED   CURRENT   READY   AGE
replicaset.apps/activator-67ffb64667              1         1         1       19m
replicaset.apps/autoscaler-7494b9b9cf             1         1         1       19m
replicaset.apps/controller-76858fd78b             1         1         1       19m
replicaset.apps/net-istio-controller-5c59fd6669   1         1         1       19m
replicaset.apps/net-istio-webhook-595d94fbb5      1         1         1       19m
replicaset.apps/webhook-59c4ddb9d                 1         1         1       19m

NAME                                            REFERENCE              TARGETS        MINPODS   MAXPODS   REPLICAS   AGE
horizontalpodautoscaler.autoscaling/activator   Deployment/activator   cpu: 1%/100%   1         20        1          19m
horizontalpodautoscaler.autoscaling/webhook     Deployment/webhook     cpu: 7%/100%   1         5         1          19m
```

```shell
k get all -n kubeflow
NAME                                                         READY   STATUS             RESTARTS        AGE
pod/admission-webhook-deployment-74b97f6c47-kn2zf            0/1     Terminating        0               21m
pod/admission-webhook-deployment-74b97f6c47-rsj9p            1/1     Running            0               14m
pod/cache-server-85444d7bb9-x56mm                            2/2     Running            0               20m
pod/centraldashboard-fbc56f468-twcfp                         2/2     Running            0               20m
pod/jupyter-web-app-deployment-548445c6b5-6992r              2/2     Running            0               20m
pod/katib-controller-64fbc9b767-whj4z                        1/1     Running            0               21m
pod/katib-db-manager-6f5b4b757c-flxlj                        0/1     CrashLoopBackOff   7 (2m54s ago)   21m
pod/katib-mysql-6d756b5657-j84fj                             0/1     Pending            0               14m
pod/katib-mysql-6d756b5657-vzqww                             0/1     Terminating        0               21m
pod/katib-ui-7678cd95ff-4bwr2                                2/2     Running            0               20m
pod/kserve-controller-manager-5fbbbcdd64-rt64n               2/2     Running            0               21m
pod/kserve-localmodel-controller-manager-5fcbb75c44-gt4km    2/2     Running            0               14m
pod/kserve-localmodel-controller-manager-5fcbb75c44-p6pk5    0/2     Terminating        0               20m
pod/kserve-models-web-app-76979487b8-rpkxt                   2/2     Running            0               20m
pod/kubeflow-pipelines-profile-controller-65d6fbc864-dkpqt   1/1     Running            0               14m
pod/kubeflow-pipelines-profile-controller-65d6fbc864-xxb4p   0/1     Terminating        0               21m
pod/metacontroller-0                                         1/1     Running            0               21m
pod/metadata-envoy-deployment-74c68d6ddc-8gd2q               0/1     Terminating        0               21m
pod/metadata-envoy-deployment-74c68d6ddc-bngdn               1/1     Running            0               14m
pod/metadata-grpc-deployment-5cc5658c5-4jw7d                 0/2     Terminating        0               20m
pod/metadata-grpc-deployment-5cc5658c5-fv8fx                 2/2     Running            0               14m
pod/metadata-writer-6d944847b8-5fwdq                         2/2     Running            2 (12m ago)     20m
pod/ml-pipeline-786f9d4b64-pzz8n                             2/2     Running            1 (15m ago)     20m
pod/ml-pipeline-persistenceagent-56d8db6f9d-x8fsb            2/2     Running            0               20m
pod/ml-pipeline-scheduledworkflow-55d77f47bd-6htkd           2/2     Running            0               20m
pod/ml-pipeline-ui-67cd999bdc-gvqhc                          0/2     Terminating        0               19m
pod/ml-pipeline-ui-67cd999bdc-nbsr8                          2/2     Running            1 (9m45s ago)   14m
pod/ml-pipeline-viewer-crd-5f9cd797dd-fjfq7                  2/2     Running            0               19m
pod/ml-pipeline-visualizationserver-57bdbc4f7f-9zn5j         2/2     Running            0               14m
pod/ml-pipeline-visualizationserver-57bdbc4f7f-vjfq2         0/2     Terminating        0               20m
pod/mysql-6c56959ffd-9wmkl                                   2/2     Running            0               20m
pod/notebook-controller-deployment-55bcfdbff9-dqgxt          2/2     Running            0               14m
pod/notebook-controller-deployment-55bcfdbff9-kf9wr          0/2     Terminating        0               20m
pod/profiles-deployment-6544b59647-2zgdv                     0/3     Terminating        0               20m
pod/profiles-deployment-6544b59647-f4mg2                     3/3     Running            0               14m
pod/pvcviewer-controller-manager-556b9c9586-bwrnn            3/3     Running            0               20m
pod/seaweedfs-b774c88f6-p2k8r                                2/2     Running            0               20m
pod/spark-operator-controller-5f44779d75-m89pg               1/1     Running            0               21m
pod/spark-operator-webhook-6744875ff-pnlt6                   1/1     Running            0               21m
pod/tensorboard-controller-deployment-5cd88b9bc8-z66qx       3/3     Running            0               20m
pod/tensorboards-web-app-deployment-7d8b47cfdd-crbg6         2/2     Running            0               14m
pod/tensorboards-web-app-deployment-7d8b47cfdd-z9xjm         0/2     Terminating        0               20m
pod/volumes-web-app-deployment-78584dbfcd-n4zjb              2/2     Running            0               20m
pod/workflow-controller-57774d58c9-4r4bh                     2/2     Running            0               14m
pod/workflow-controller-57774d58c9-9vlgq                     0/2     Terminating        0               20m

NAME                                                                TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                                                   AGE
service/admission-webhook-service                                   ClusterIP   10.43.36.112    <none>        443/TCP                                                   22m
service/cache-server                                                ClusterIP   10.43.234.123   <none>        443/TCP                                                   22m
service/centraldashboard                                            ClusterIP   10.43.84.252    <none>        80/TCP                                                    21m
service/jupyter-web-app-service                                     ClusterIP   10.43.97.207    <none>        80/TCP                                                    21m
service/katib-controller                                            ClusterIP   10.43.2.96      <none>        443/TCP,8080/TCP,18080/TCP                                21m
service/katib-db-manager                                            ClusterIP   10.43.208.221   <none>        6789/TCP                                                  21m
service/katib-mysql                                                 ClusterIP   10.43.111.161   <none>        3306/TCP                                                  21m
service/katib-ui                                                    ClusterIP   10.43.79.131    <none>        80/TCP                                                    21m
service/kserve-controller-manager-metrics-service                   ClusterIP   10.43.41.64     <none>        8443/TCP                                                  21m
service/kserve-controller-manager-service                           ClusterIP   10.43.202.36    <none>        8443/TCP                                                  21m
service/kserve-models-web-app                                       ClusterIP   10.43.85.20     <none>        80/TCP                                                    21m
service/kserve-webhook-server-service                               ClusterIP   10.43.37.71     <none>        443/TCP                                                   21m
service/kubeflow-pipelines-profile-controller                       ClusterIP   10.43.162.30    <none>        80/TCP                                                    21m
service/metadata-envoy-service                                      ClusterIP   10.43.208.189   <none>        9090/TCP                                                  21m
service/metadata-grpc-service                                       ClusterIP   10.43.40.105    <none>        8080/TCP                                                  21m
service/minio-service                                               ClusterIP   10.43.255.211   <none>        9000/TCP                                                  21m
service/ml-pipeline                                                 ClusterIP   10.43.102.186   <none>        8888/TCP,8887/TCP                                         21m
service/ml-pipeline-ui                                              ClusterIP   10.43.8.155     <none>        80/TCP                                                    21m
service/ml-pipeline-visualizationserver                             ClusterIP   10.43.247.116   <none>        8888/TCP                                                  21m
service/mysql                                                       ClusterIP   10.43.240.208   <none>        3306/TCP                                                  21m
service/notebook-controller-service                                 ClusterIP   10.43.37.219    <none>        443/TCP                                                   21m
service/profiles-kfam                                               ClusterIP   10.43.109.23    <none>        8081/TCP                                                  21m
service/pvcviewer-controller-manager-metrics-service                ClusterIP   10.43.18.120    <none>        8443/TCP                                                  21m
service/pvcviewer-webhook-service                                   ClusterIP   10.43.68.123    <none>        443/TCP                                                   21m
service/seaweedfs                                                   ClusterIP   10.43.240.216   <none>        8111/TCP,8333/TCP,9333/TCP,19333/TCP,18888/TCP,8888/TCP   21m
service/spark-operator-webhook-svc                                  ClusterIP   10.43.38.240    <none>        9443/TCP                                                  21m
service/tensorboard-controller-controller-manager-metrics-service   ClusterIP   10.43.96.201    <none>        8443/TCP                                                  21m
service/tensorboards-web-app-service                                ClusterIP   10.43.202.1     <none>        80/TCP                                                    21m
service/volumes-web-app-service                                     ClusterIP   10.43.211.117   <none>        80/TCP                                                    21m

NAME                                                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/admission-webhook-deployment            1/1     1            1           21m
deployment.apps/cache-server                            1/1     1            1           21m
deployment.apps/centraldashboard                        1/1     1            1           21m
deployment.apps/jupyter-web-app-deployment              1/1     1            1           21m
deployment.apps/katib-controller                        1/1     1            1           21m
deployment.apps/katib-db-manager                        0/1     1            0           21m
deployment.apps/katib-mysql                             0/1     1            0           21m
deployment.apps/katib-ui                                1/1     1            1           21m
deployment.apps/kserve-controller-manager               1/1     1            1           21m
deployment.apps/kserve-localmodel-controller-manager    1/1     1            1           21m
deployment.apps/kserve-models-web-app                   1/1     1            1           21m
deployment.apps/kubeflow-pipelines-profile-controller   1/1     1            1           21m
deployment.apps/metadata-envoy-deployment               1/1     1            1           21m
deployment.apps/metadata-grpc-deployment                1/1     1            1           21m
deployment.apps/metadata-writer                         1/1     1            1           21m
deployment.apps/ml-pipeline                             1/1     1            1           21m
deployment.apps/ml-pipeline-persistenceagent            1/1     1            1           21m
deployment.apps/ml-pipeline-scheduledworkflow           1/1     1            1           21m
deployment.apps/ml-pipeline-ui                          1/1     1            1           21m
deployment.apps/ml-pipeline-viewer-crd                  1/1     1            1           21m
deployment.apps/ml-pipeline-visualizationserver         1/1     1            1           21m
deployment.apps/mysql                                   1/1     1            1           21m
deployment.apps/notebook-controller-deployment          1/1     1            1           21m
deployment.apps/profiles-deployment                     1/1     1            1           21m
deployment.apps/pvcviewer-controller-manager            1/1     1            1           21m
deployment.apps/seaweedfs                               1/1     1            1           21m
deployment.apps/spark-operator-controller               1/1     1            1           21m
deployment.apps/spark-operator-webhook                  1/1     1            1           21m
deployment.apps/tensorboard-controller-deployment       1/1     1            1           21m
deployment.apps/tensorboards-web-app-deployment         1/1     1            1           21m
deployment.apps/volumes-web-app-deployment              1/1     1            1           21m
deployment.apps/workflow-controller                     1/1     1            1           21m

NAME                                                               DESIRED   CURRENT   READY   AGE
replicaset.apps/admission-webhook-deployment-74b97f6c47            1         1         1       21m
replicaset.apps/cache-server-85444d7bb9                            1         1         1       21m
replicaset.apps/centraldashboard-fbc56f468                         1         1         1       21m
replicaset.apps/jupyter-web-app-deployment-548445c6b5              1         1         1       21m
replicaset.apps/katib-controller-64fbc9b767                        1         1         1       21m
replicaset.apps/katib-db-manager-6f5b4b757c                        1         1         0       21m
replicaset.apps/katib-mysql-6d756b5657                             1         1         0       21m
replicaset.apps/katib-ui-7678cd95ff                                1         1         1       21m
replicaset.apps/kserve-controller-manager-5fbbbcdd64               1         1         1       21m
replicaset.apps/kserve-localmodel-controller-manager-5fcbb75c44    1         1         1       21m
replicaset.apps/kserve-models-web-app-76979487b8                   1         1         1       21m
replicaset.apps/kubeflow-pipelines-profile-controller-65d6fbc864   1         1         1       21m
replicaset.apps/metadata-envoy-deployment-74c68d6ddc               1         1         1       21m
replicaset.apps/metadata-grpc-deployment-5cc5658c5                 1         1         1       21m
replicaset.apps/metadata-writer-6d944847b8                         1         1         1       21m
replicaset.apps/ml-pipeline-786f9d4b64                             1         1         1       21m
replicaset.apps/ml-pipeline-persistenceagent-56d8db6f9d            1         1         1       21m
replicaset.apps/ml-pipeline-scheduledworkflow-55d77f47bd           1         1         1       21m
replicaset.apps/ml-pipeline-ui-67cd999bdc                          1         1         1       21m
replicaset.apps/ml-pipeline-viewer-crd-5f9cd797dd                  1         1         1       21m
replicaset.apps/ml-pipeline-visualizationserver-57bdbc4f7f         1         1         1       21m
replicaset.apps/mysql-6c56959ffd                                   1         1         1       21m
replicaset.apps/notebook-controller-deployment-55bcfdbff9          1         1         1       21m
replicaset.apps/profiles-deployment-6544b59647                     1         1         1       21m
replicaset.apps/pvcviewer-controller-manager-556b9c9586            1         1         1       21m
replicaset.apps/seaweedfs-b774c88f6                                1         1         1       21m
replicaset.apps/spark-operator-controller-5f44779d75               1         1         1       21m
replicaset.apps/spark-operator-webhook-6744875ff                   1         1         1       21m
replicaset.apps/tensorboard-controller-deployment-5cd88b9bc8       1         1         1       21m
replicaset.apps/tensorboards-web-app-deployment-7d8b47cfdd         1         1         1       21m
replicaset.apps/volumes-web-app-deployment-78584dbfcd              1         1         1       21m
replicaset.apps/workflow-controller-57774d58c9                     1         1         1       21m

NAME                              READY   AGE
statefulset.apps/metacontroller   1/1     21m
```

```shell
k get all -n kubeflow-system
NAME                                                       READY   STATUS        RESTARTS   AGE
pod/jobset-controller-manager-79598d8d4b-sc9vs             0/2     Terminating   0          21m
pod/jobset-controller-manager-79598d8d4b-wqpl5             2/2     Running       0          16m
pod/kubeflow-trainer-controller-manager-7f8df97c8c-nhnhf   2/2     Running       0          21m

NAME                                                TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)            AGE
service/jobset-controller-manager-metrics-service   ClusterIP   10.43.200.140   <none>        8443/TCP           23m
service/jobset-webhook-service                      ClusterIP   10.43.42.150    <none>        443/TCP            23m
service/kubeflow-trainer-controller-manager         ClusterIP   10.43.29.169    <none>        8080/TCP,443/TCP   23m

NAME                                                  READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/jobset-controller-manager             1/1     1            1           23m
deployment.apps/kubeflow-trainer-controller-manager   1/1     1            1           23m

NAME                                                             DESIRED   CURRENT   READY   AGE
replicaset.apps/jobset-controller-manager-79598d8d4b             1         1         1       23m
replicaset.apps/kubeflow-trainer-controller-manager-7f8df97c8c   1         1         1       23m
```

```shell
 k get all -n kubeflow-system
NAME                                                       READY   STATUS        RESTARTS   AGE
pod/jobset-controller-manager-79598d8d4b-sc9vs             0/2     Terminating   0          21m
pod/jobset-controller-manager-79598d8d4b-wqpl5             2/2     Running       0          16m
pod/kubeflow-trainer-controller-manager-7f8df97c8c-nhnhf   2/2     Running       0          21m

NAME                                                TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)            AGE
service/jobset-controller-manager-metrics-service   ClusterIP   10.43.200.140   <none>        8443/TCP           23m
service/jobset-webhook-service                      ClusterIP   10.43.42.150    <none>        443/TCP            23m
service/kubeflow-trainer-controller-manager         ClusterIP   10.43.29.169    <none>        8080/TCP,443/TCP   23m

NAME                                                  READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/jobset-controller-manager             1/1     1            1           23m
deployment.apps/kubeflow-trainer-controller-manager   1/1     1            1           23m

NAME                                                             DESIRED   CURRENT   READY   AGE
replicaset.apps/jobset-controller-manager-79598d8d4b             1         1         1       23m
replicaset.apps/kubeflow-trainer-controller-manager-7f8df97c8c   1         1         1       23m
kim@kim-Latitude-5430:~$ k get all -n oauth2-proxy
NAME                               READY   STATUS        RESTARTS   AGE
pod/oauth2-proxy-c696dfff5-jlc2g   1/1     Running       0          23m
pod/oauth2-proxy-c696dfff5-jqgxb   0/1     Terminating   0          23m
pod/oauth2-proxy-c696dfff5-ql94b   1/1     Running       0          16m

NAME                   TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
service/oauth2-proxy   ClusterIP   10.43.237.209   <none>        80/TCP    23m

NAME                           READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/oauth2-proxy   2/2     2            2           23m

NAME                                     DESIRED   CURRENT   READY   AGE
replicaset.apps/oauth2-proxy-c696dfff5   2         2         2       23m
```

