# deploy to GCE sucess:
1.	Error permission Elasticsearch.
2. 	Error PVC insufficient memory
3.	Error ss-secret not found
4.	Error cannot pull the images:latest 

The working log: 


`<
Last login: Thu Nov  1 23:02:30 on ttys003
Hungs-MBP:~ hungbang$ gcloud 
alpha                debug                kms 
app                  deployment-manager   logging 
auth                 dns                  ml 
beta                 docker               ml-engine 
bigtable             domains              organizations 
builds               endpoints            projects 
components           feedback             pubsub 
composer             firebase             redis 
compute              functions            services 
config               help                 source 
container            iam                  spanner 
dataflow             info                 sql 
dataproc             init                 topic 
datastore            iot                  version 
Hungs-MBP:~ hungbang$ gcloud 
alpha                debug                kms 
app                  deployment-manager   logging 
auth                 dns                  ml 
beta                 docker               ml-engine 
bigtable             domains              organizations 
builds               endpoints            projects 
components           feedback             pubsub 
composer             firebase             redis 
compute              functions            services 
config               help                 source 
container            iam                  spanner 
dataflow             info                 sql 
dataproc             init                 topic 
datastore            iot                  version 
Hungs-MBP:~ hungbang$ gcloud 
alpha                debug                kms 
app                  deployment-manager   logging 
auth                 dns                  ml 
beta                 docker               ml-engine 
bigtable             domains              organizations 
builds               endpoints            projects 
components           feedback             pubsub 
composer             firebase             redis 
compute              functions            services 
config               help                 source 
container            iam                  spanner 
dataflow             info                 sql 
dataproc             init                 topic 
datastore            iot                  version 
Hungs-MBP:~ hungbang$ gcloud container clusters get-credentials cloud-build-screening
Fetching cluster endpoint and auth data.
ERROR: (gcloud.container.clusters.get-credentials) ResponseError: code=404, message=Not found: projects/sanctionscreen/zones/us-east1-b/clusters/cloud-build-screening.
Could not find [cloud-build-screening] in [us-east1-b].
Did you mean [cloud-build-screening] in [us-central1-b]?
Hungs-MBP:~ hungbang$ gcloud container clusters get-credentials cloud-build-screening --zone=us-central1-b
Fetching cluster endpoint and auth data.
kubeconfig entry generated for cloud-build-screening.
Hungs-MBP:~ hungbang$ kubectl get pods
NAME                             READY     STATUS             RESTARTS   AGE
elasticsearch-57668d4b8c-bf7jh   0/1       CrashLoopBackOff   7          14m
kibana-986f6847f-v67v9           1/1       Running            0          1h
redis-9dcd8d797-7khrz            1/1       Running            0          1h
Hungs-MBP:~ hungbang$ kubectl logs elasticsearch-57668d4b8c-bf7jh -p
OpenJDK 64-Bit Server VM warning: If the number of processors is expected to increase from one, then you should configure the number of parallel GC threads appropriately using -XX:ParallelGCThreads=N
[2018-11-01T16:10:00,453][WARN ][o.e.b.JNANatives         ] Unable to lock JVM Memory: error=12, reason=Cannot allocate memory
[2018-11-01T16:10:00,456][WARN ][o.e.b.JNANatives         ] This can result in part of the JVM being swapped out.
[2018-11-01T16:10:00,456][WARN ][o.e.b.JNANatives         ] Increase RLIMIT_MEMLOCK, soft limit: 65536, hard limit: 65536
[2018-11-01T16:10:00,457][WARN ][o.e.b.JNANatives         ] These can be adjusted by modifying /etc/security/limits.conf, for example: 
	# allow user 'elasticsearch' mlockall
	elasticsearch soft memlock unlimited
	elasticsearch hard memlock unlimited
[2018-11-01T16:10:00,457][WARN ][o.e.b.JNANatives         ] If you are logged in interactively, you will have to re-login for the new limits to take effect.
[2018-11-01T16:10:00,766][INFO ][o.e.n.Node               ] [] initializing ...
[2018-11-01T16:10:00,819][WARN ][o.e.b.ElasticsearchUncaughtExceptionHandler] [] uncaught exception in thread [main]
org.elasticsearch.bootstrap.StartupException: java.lang.IllegalStateException: Failed to created node environment
	at org.elasticsearch.bootstrap.Elasticsearch.init(Elasticsearch.java:127) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Elasticsearch.execute(Elasticsearch.java:114) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.cli.EnvironmentAwareCommand.execute(EnvironmentAwareCommand.java:67) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.cli.Command.mainWithoutErrorHandling(Command.java:122) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.cli.Command.main(Command.java:88) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Elasticsearch.main(Elasticsearch.java:91) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Elasticsearch.main(Elasticsearch.java:84) ~[elasticsearch-5.4.3.jar:5.4.3]
Caused by: java.lang.IllegalStateException: Failed to created node environment
	at org.elasticsearch.node.Node.<init>(Node.java:265) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.node.Node.<init>(Node.java:242) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Bootstrap$5.<init>(Bootstrap.java:232) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Bootstrap.setup(Bootstrap.java:232) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Bootstrap.init(Bootstrap.java:350) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Elasticsearch.init(Elasticsearch.java:123) ~[elasticsearch-5.4.3.jar:5.4.3]
	... 6 more
Caused by: java.nio.file.AccessDeniedException: /usr/share/elasticsearch/data/nodes
	at sun.nio.fs.UnixException.translateToIOException(UnixException.java:84) ~[?:?]
	at sun.nio.fs.UnixException.rethrowAsIOException(UnixException.java:102) ~[?:?]
	at sun.nio.fs.UnixException.rethrowAsIOException(UnixException.java:107) ~[?:?]
	at sun.nio.fs.UnixFileSystemProvider.createDirectory(UnixFileSystemProvider.java:384) ~[?:?]
	at java.nio.file.Files.createDirectory(Files.java:674) ~[?:1.8.0_131]
	at java.nio.file.Files.createAndCheckIsDirectory(Files.java:781) ~[?:1.8.0_131]
	at java.nio.file.Files.createDirectories(Files.java:767) ~[?:1.8.0_131]
	at org.elasticsearch.env.NodeEnvironment.<init>(NodeEnvironment.java:221) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.node.Node.<init>(Node.java:262) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.node.Node.<init>(Node.java:242) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Bootstrap$5.<init>(Bootstrap.java:232) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Bootstrap.setup(Bootstrap.java:232) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Bootstrap.init(Bootstrap.java:350) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Elasticsearch.init(Elasticsearch.java:123) ~[elasticsearch-5.4.3.jar:5.4.3]
	... 6 more
Hungs-MBP:~ hungbang$ kubectl logs -f elasticsearch-57668d4b8c-bf7jh
OpenJDK 64-Bit Server VM warning: If the number of processors is expected to increase from one, then you should configure the number of parallel GC threads appropriately using -XX:ParallelGCThreads=N
[2018-11-01T16:15:06,169][WARN ][o.e.b.JNANatives         ] Unable to lock JVM Memory: error=12, reason=Cannot allocate memory
[2018-11-01T16:15:06,172][WARN ][o.e.b.JNANatives         ] This can result in part of the JVM being swapped out.
[2018-11-01T16:15:06,172][WARN ][o.e.b.JNANatives         ] Increase RLIMIT_MEMLOCK, soft limit: 65536, hard limit: 65536
[2018-11-01T16:15:06,173][WARN ][o.e.b.JNANatives         ] These can be adjusted by modifying /etc/security/limits.conf, for example: 
	# allow user 'elasticsearch' mlockall
	elasticsearch soft memlock unlimited
	elasticsearch hard memlock unlimited
[2018-11-01T16:15:06,177][WARN ][o.e.b.JNANatives         ] If you are logged in interactively, you will have to re-login for the new limits to take effect.
[2018-11-01T16:15:06,467][INFO ][o.e.n.Node               ] [] initializing ...
[2018-11-01T16:15:06,509][WARN ][o.e.b.ElasticsearchUncaughtExceptionHandler] [] uncaught exception in thread [main]
org.elasticsearch.bootstrap.StartupException: java.lang.IllegalStateException: Failed to created node environment
	at org.elasticsearch.bootstrap.Elasticsearch.init(Elasticsearch.java:127) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Elasticsearch.execute(Elasticsearch.java:114) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.cli.EnvironmentAwareCommand.execute(EnvironmentAwareCommand.java:67) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.cli.Command.mainWithoutErrorHandling(Command.java:122) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.cli.Command.main(Command.java:88) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Elasticsearch.main(Elasticsearch.java:91) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Elasticsearch.main(Elasticsearch.java:84) ~[elasticsearch-5.4.3.jar:5.4.3]
Caused by: java.lang.IllegalStateException: Failed to created node environment
	at org.elasticsearch.node.Node.<init>(Node.java:265) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.node.Node.<init>(Node.java:242) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Bootstrap$5.<init>(Bootstrap.java:232) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Bootstrap.setup(Bootstrap.java:232) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Bootstrap.init(Bootstrap.java:350) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Elasticsearch.init(Elasticsearch.java:123) ~[elasticsearch-5.4.3.jar:5.4.3]
	... 6 more
Caused by: java.nio.file.AccessDeniedException: /usr/share/elasticsearch/data/nodes
	at sun.nio.fs.UnixException.translateToIOException(UnixException.java:84) ~[?:?]
	at sun.nio.fs.UnixException.rethrowAsIOException(UnixException.java:102) ~[?:?]
	at sun.nio.fs.UnixException.rethrowAsIOException(UnixException.java:107) ~[?:?]
	at sun.nio.fs.UnixFileSystemProvider.createDirectory(UnixFileSystemProvider.java:384) ~[?:?]
	at java.nio.file.Files.createDirectory(Files.java:674) ~[?:1.8.0_131]
	at java.nio.file.Files.createAndCheckIsDirectory(Files.java:781) ~[?:1.8.0_131]
	at java.nio.file.Files.createDirectories(Files.java:767) ~[?:1.8.0_131]
	at org.elasticsearch.env.NodeEnvironment.<init>(NodeEnvironment.java:221) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.node.Node.<init>(Node.java:262) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.node.Node.<init>(Node.java:242) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Bootstrap$5.<init>(Bootstrap.java:232) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Bootstrap.setup(Bootstrap.java:232) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Bootstrap.init(Bootstrap.java:350) ~[elasticsearch-5.4.3.jar:5.4.3]
	at org.elasticsearch.bootstrap.Elasticsearch.init(Elasticsearch.java:123) ~[elasticsearch-5.4.3.jar:5.4.3]
	... 6 more
Hungs-MBP:~ hungbang$ kubectl get pods
NAME                             READY     STATUS             RESTARTS   AGE
elasticsearch-57668d4b8c-bf7jh   0/1       CrashLoopBackOff   9          22m
kibana-986f6847f-v67v9           1/1       Running            0          1h
redis-9dcd8d797-7khrz            1/1       Running            0          1h
Hungs-MBP:~ hungbang$ kubectl get clusterrolebinding
NAME                                                   AGE
cluster-admin                                          37d
event-exporter-rb                                      37d
gce:beta:kubelet-certificate-bootstrap                 37d
gce:beta:kubelet-certificate-rotation                  37d
heapster-binding                                       37d
kube-apiserver-kubelet-api-admin                       37d
kubelet-bootstrap                                      37d
kubelet-cluster-admin                                  37d
metrics-server:system:auth-delegator                   37d
npd-binding                                            37d
system:aws-cloud-provider                              37d
system:basic-user                                      37d
system:controller:attachdetach-controller              37d
system:controller:certificate-controller               37d
system:controller:clusterrole-aggregation-controller   37d
system:controller:cronjob-controller                   37d
system:controller:daemon-set-controller                37d
system:controller:deployment-controller                37d
system:controller:disruption-controller                37d
system:controller:endpoint-controller                  37d
system:controller:generic-garbage-collector            37d
system:controller:horizontal-pod-autoscaler            37d
system:controller:job-controller                       37d
system:controller:namespace-controller                 37d
system:controller:node-controller                      37d
system:controller:persistent-volume-binder             37d
system:controller:pod-garbage-collector                37d
system:controller:pv-protection-controller             37d
system:controller:pvc-protection-controller            37d
system:controller:replicaset-controller                37d
system:controller:replication-controller               37d
system:controller:resourcequota-controller             37d
system:controller:route-controller                     37d
system:controller:service-account-controller           37d
system:controller:service-controller                   37d
system:controller:statefulset-controller               37d
system:controller:ttl-controller                       37d
system:discovery                                       37d
system:kube-controller-manager                         37d
system:kube-dns                                        37d
system:kube-dns-autoscaler                             37d
system:kube-scheduler                                  37d
system:metrics-server                                  37d
system:node                                            37d
system:node-proxier                                    37d
Hungs-MBP:~ hungbang$ gcloud info | grep Account
Account: [quanhungbang@gmail.com]
    account: [quanhungbang@gmail.com]
Hungs-MBP:~ hungbang$ cd Public/projects/screening/
Hungs-MBP:screening hungbang$ kubectl get deployment
NAME            DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
elasticsearch   1         1         1            0           39m
kibana          1         1         1            1           1h
redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl delete deployment elasticsearch
deployment.extensions "elasticsearch" deleted
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS        RESTARTS   AGE
pod/elasticsearch-57668d4b8c-bf7jh   0/1       Terminating   12         40m
pod/kibana-986f6847f-v67v9           1/1       Running       0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running       0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                           DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/kibana   1         1         1            1           1h
deployment.extensions/redis    1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                         READY     STATUS    RESTARTS   AGE
pod/kibana-986f6847f-v67v9   1/1       Running   0          1h
pod/redis-9dcd8d797-7khrz    1/1       Running   0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                           DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/kibana   1         1         1            1           1h
deployment.extensions/redis    1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl apply -f k8s-elasticsearch/elasticsearch-deployment.yaml 
deployment.extensions/elasticsearch created
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS     RESTARTS   AGE
pod/elasticsearch-598ff57f45-5h7dd   0/1       Init:0/3   0          3s
pod/kibana-986f6847f-v67v9           1/1       Running    0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running    0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/elasticsearch   1         1         1            0           3s
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS     RESTARTS   AGE
pod/elasticsearch-598ff57f45-5h7dd   0/1       Init:0/3   0          8s
pod/kibana-986f6847f-v67v9           1/1       Running    0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running    0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/elasticsearch   1         1         1            0           8s
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl describe pod elasticsearch-598ff57f45-5h7dd
Name:           elasticsearch-598ff57f45-5h7dd
Namespace:      default
Node:           gke-cloud-build-screenin-default-pool-d23c46b8-2hm7/10.128.0.3
Start Time:     Thu, 01 Nov 2018 23:39:12 +0700
Labels:         io.kompose.service=elasticsearch
                pod-template-hash=1549913901
Annotations:    kubernetes.io/limit-ranger=LimitRanger plugin set: cpu request for container ss-elasticsearch; cpu request for init container fix-the-volume-permission; cpu request for init container increase-the-vm-...
Status:         Pending
IP:             10.20.1.7
Controlled By:  ReplicaSet/elasticsearch-598ff57f45
Init Containers:
  fix-the-volume-permission:
    Container ID:  docker://ae2b2c8a40b9d651e1f37376882aa1659751cf8aa3df862176456643eff17128
    Image:         busybox
    Image ID:      docker-pullable://busybox@sha256:915f390a8912e16d4beb8689720a17348f3f6d1a7b659697df850ab625ea29d5
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      chown -R 1000:1000 /usr/share/elasticsearch/data
    State:          Waiting
      Reason:       CrashLoopBackOff
    Last State:     Terminated
      Reason:       Error
      Exit Code:    1
      Started:      Thu, 01 Nov 2018 23:39:22 +0700
      Finished:     Thu, 01 Nov 2018 23:39:22 +0700
    Ready:          False
    Restart Count:  1
    Requests:
      cpu:        100m
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
  increase-the-vm-max-map-count:
    Container ID:  
    Image:         busybox
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sysctl
      -w
      vm.max_map_count=262144
    State:          Waiting
      Reason:       PodInitializing
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:        100m
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
  increase-the-ulimit:
    Container ID:  
    Image:         busybox
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      ulimit -n 65536
    State:          Waiting
      Reason:       PodInitializing
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:        100m
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
Containers:
  ss-elasticsearch:
    Container ID:   
    Image:          docker.elastic.co/elasticsearch/elasticsearch:5.4.3
    Image ID:       
    Ports:          9300/TCP, 9200/TCP
    Host Ports:     0/TCP, 0/TCP
    State:          Waiting
      Reason:       PodInitializing
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:  100m
    Environment:
      ES_JAVA_OPTS:                  -Xms2g -Xmx2g
      bootstrap.memory_lock:         true
      bootstrap.system_call_filter:  false
      cluster.name:                  ss-cluster
      discovery.type:                single-node
      http.host:                     0.0.0.0
      http.port:                     9200
      network.host:                  0.0.0.0
      network.publish_host:          0.0.0.0
      xpack.graph.enabled:           false
      xpack.monitoring.enabled:      false
      xpack.security.enabled:        false
      xpack.watcher.enabled:         false
    Mounts:
      /usr/share/elasticsearch/data from esdata (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
Conditions:
  Type           Status
  Initialized    False 
  Ready          False 
  PodScheduled   True 
Volumes:
  esdata:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  esdata
    ReadOnly:   false
  default-token-4kxcq:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-4kxcq
    Optional:    false
QoS Class:       Burstable
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age                From                                                          Message
  ----     ------                 ----               ----                                                          -------
  Normal   Scheduled              22s                default-scheduler                                             Successfully assigned elasticsearch-598ff57f45-5h7dd to gke-cloud-build-screenin-default-pool-d23c46b8-2hm7
  Normal   SuccessfulMountVolume  22s                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "default-token-4kxcq"
  Normal   SuccessfulMountVolume  13s                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "pvc-11f0ea1f-ddea-11e8-b1ae-42010a80008b"
  Normal   Pulling                12s (x2 over 13s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  pulling image "busybox"
  Normal   Pulled                 12s (x2 over 13s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Successfully pulled image "busybox"
  Normal   Created                12s (x2 over 13s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Created container
  Normal   Started                12s (x2 over 13s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Started container
  Warning  BackOff                10s (x2 over 11s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Back-off restarting failed container
Hungs-MBP:screening hungbang$ kubectl describe pod elasticsearch-598ff57f45-5h7dd
Name:           elasticsearch-598ff57f45-5h7dd
Namespace:      default
Node:           gke-cloud-build-screenin-default-pool-d23c46b8-2hm7/10.128.0.3
Start Time:     Thu, 01 Nov 2018 23:39:12 +0700
Labels:         io.kompose.service=elasticsearch
                pod-template-hash=1549913901
Annotations:    kubernetes.io/limit-ranger=LimitRanger plugin set: cpu request for container ss-elasticsearch; cpu request for init container fix-the-volume-permission; cpu request for init container increase-the-vm-...
Status:         Pending
IP:             10.20.1.7
Controlled By:  ReplicaSet/elasticsearch-598ff57f45
Init Containers:
  fix-the-volume-permission:
    Container ID:  docker://39fa15b120c9dd69bd7dee00c7e3366da16fc0a155585f0279a419ca3f013c59
    Image:         busybox
    Image ID:      docker-pullable://busybox@sha256:915f390a8912e16d4beb8689720a17348f3f6d1a7b659697df850ab625ea29d5
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      chown -R 1000:1000 /usr/share/elasticsearch/data
    State:          Terminated
      Reason:       Error
      Exit Code:    1
      Started:      Thu, 01 Nov 2018 23:39:37 +0700
      Finished:     Thu, 01 Nov 2018 23:39:37 +0700
    Last State:     Terminated
      Reason:       Error
      Exit Code:    1
      Started:      Thu, 01 Nov 2018 23:39:22 +0700
      Finished:     Thu, 01 Nov 2018 23:39:22 +0700
    Ready:          False
    Restart Count:  2
    Requests:
      cpu:        100m
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
  increase-the-vm-max-map-count:
    Container ID:  
    Image:         busybox
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sysctl
      -w
      vm.max_map_count=262144
    State:          Waiting
      Reason:       PodInitializing
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:        100m
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
  increase-the-ulimit:
    Container ID:  
    Image:         busybox
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      ulimit -n 65536
    State:          Waiting
      Reason:       PodInitializing
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:        100m
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
Containers:
  ss-elasticsearch:
    Container ID:   
    Image:          docker.elastic.co/elasticsearch/elasticsearch:5.4.3
    Image ID:       
    Ports:          9300/TCP, 9200/TCP
    Host Ports:     0/TCP, 0/TCP
    State:          Waiting
      Reason:       PodInitializing
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:  100m
    Environment:
      ES_JAVA_OPTS:                  -Xms2g -Xmx2g
      bootstrap.memory_lock:         true
      bootstrap.system_call_filter:  false
      cluster.name:                  ss-cluster
      discovery.type:                single-node
      http.host:                     0.0.0.0
      http.port:                     9200
      network.host:                  0.0.0.0
      network.publish_host:          0.0.0.0
      xpack.graph.enabled:           false
      xpack.monitoring.enabled:      false
      xpack.security.enabled:        false
      xpack.watcher.enabled:         false
    Mounts:
      /usr/share/elasticsearch/data from esdata (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
Conditions:
  Type           Status
  Initialized    False 
  Ready          False 
  PodScheduled   True 
Volumes:
  esdata:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  esdata
    ReadOnly:   false
  default-token-4kxcq:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-4kxcq
    Optional:    false
QoS Class:       Burstable
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age                From                                                          Message
  ----     ------                 ----               ----                                                          -------
  Normal   Scheduled              36s                default-scheduler                                             Successfully assigned elasticsearch-598ff57f45-5h7dd to gke-cloud-build-screenin-default-pool-d23c46b8-2hm7
  Normal   SuccessfulMountVolume  36s                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "default-token-4kxcq"
  Normal   SuccessfulMountVolume  27s                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "pvc-11f0ea1f-ddea-11e8-b1ae-42010a80008b"
  Normal   Pulling                12s (x3 over 27s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  pulling image "busybox"
  Normal   Pulled                 11s (x3 over 27s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Successfully pulled image "busybox"
  Normal   Created                11s (x3 over 27s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Created container
  Normal   Started                11s (x3 over 27s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Started container
  Warning  BackOff                11s (x3 over 25s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Back-off restarting failed container
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS                  RESTARTS   AGE
pod/elasticsearch-598ff57f45-5h7dd   0/1       Init:CrashLoopBackOff   2          41s
pod/kibana-986f6847f-v67v9           1/1       Running                 0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running                 0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/elasticsearch   1         1         1            0           41s
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS                  RESTARTS   AGE
pod/elasticsearch-598ff57f45-5h7dd   0/1       Init:CrashLoopBackOff   3          1m
pod/kibana-986f6847f-v67v9           1/1       Running                 0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running                 0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/elasticsearch   1         1         1            0           1m
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl logs -f elasticsearch-598ff57f45-5h7dd
Error from server (BadRequest): container "ss-elasticsearch" in pod "elasticsearch-598ff57f45-5h7dd" is waiting to start: PodInitializing
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS                  RESTARTS   AGE
pod/elasticsearch-598ff57f45-5h7dd   0/1       Init:CrashLoopBackOff   3          1m
pod/kibana-986f6847f-v67v9           1/1       Running                 0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running                 0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/elasticsearch   1         1         1            0           1m
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl describe pod elasticsearch-598ff57f45-5h7dd
Name:           elasticsearch-598ff57f45-5h7dd
Namespace:      default
Node:           gke-cloud-build-screenin-default-pool-d23c46b8-2hm7/10.128.0.3
Start Time:     Thu, 01 Nov 2018 23:39:12 +0700
Labels:         io.kompose.service=elasticsearch
                pod-template-hash=1549913901
Annotations:    kubernetes.io/limit-ranger=LimitRanger plugin set: cpu request for container ss-elasticsearch; cpu request for init container fix-the-volume-permission; cpu request for init container increase-the-vm-...
Status:         Pending
IP:             10.20.1.7
Controlled By:  ReplicaSet/elasticsearch-598ff57f45
Init Containers:
  fix-the-volume-permission:
    Container ID:  docker://46e9d003b0e6d27b4a7d46784b56380ee15910f78cc9bd06c4b4d2e1ce363010
    Image:         busybox
    Image ID:      docker-pullable://busybox@sha256:915f390a8912e16d4beb8689720a17348f3f6d1a7b659697df850ab625ea29d5
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      chown -R 1000:1000 /usr/share/elasticsearch/data
    State:          Waiting
      Reason:       CrashLoopBackOff
    Last State:     Terminated
      Reason:       Error
      Exit Code:    1
      Started:      Thu, 01 Nov 2018 23:40:01 +0700
      Finished:     Thu, 01 Nov 2018 23:40:01 +0700
    Ready:          False
    Restart Count:  3
    Requests:
      cpu:        100m
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
  increase-the-vm-max-map-count:
    Container ID:  
    Image:         busybox
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sysctl
      -w
      vm.max_map_count=262144
    State:          Waiting
      Reason:       PodInitializing
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:        100m
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
  increase-the-ulimit:
    Container ID:  
    Image:         busybox
    Image ID:      
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      ulimit -n 65536
    State:          Waiting
      Reason:       PodInitializing
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:        100m
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
Containers:
  ss-elasticsearch:
    Container ID:   
    Image:          docker.elastic.co/elasticsearch/elasticsearch:5.4.3
    Image ID:       
    Ports:          9300/TCP, 9200/TCP
    Host Ports:     0/TCP, 0/TCP
    State:          Waiting
      Reason:       PodInitializing
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:  100m
    Environment:
      ES_JAVA_OPTS:                  -Xms2g -Xmx2g
      bootstrap.memory_lock:         true
      bootstrap.system_call_filter:  false
      cluster.name:                  ss-cluster
      discovery.type:                single-node
      http.host:                     0.0.0.0
      http.port:                     9200
      network.host:                  0.0.0.0
      network.publish_host:          0.0.0.0
      xpack.graph.enabled:           false
      xpack.monitoring.enabled:      false
      xpack.security.enabled:        false
      xpack.watcher.enabled:         false
    Mounts:
      /usr/share/elasticsearch/data from esdata (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
Conditions:
  Type           Status
  Initialized    False 
  Ready          False 
  PodScheduled   True 
Volumes:
  esdata:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  esdata
    ReadOnly:   false
  default-token-4kxcq:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-4kxcq
    Optional:    false
QoS Class:       Burstable
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age               From                                                          Message
  ----     ------                 ----              ----                                                          -------
  Normal   Scheduled              1m                default-scheduler                                             Successfully assigned elasticsearch-598ff57f45-5h7dd to gke-cloud-build-screenin-default-pool-d23c46b8-2hm7
  Normal   SuccessfulMountVolume  1m                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "default-token-4kxcq"
  Normal   SuccessfulMountVolume  1m                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "pvc-11f0ea1f-ddea-11e8-b1ae-42010a80008b"
  Normal   Pulling                50s (x4 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  pulling image "busybox"
  Normal   Pulled                 49s (x4 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Successfully pulled image "busybox"
  Normal   Created                49s (x4 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Created container
  Normal   Started                49s (x4 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Started container
  Warning  BackOff                25s (x7 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Back-off restarting failed container
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS       RESTARTS   AGE
pod/elasticsearch-598ff57f45-5h7dd   0/1       Init:Error   4          1m
pod/kibana-986f6847f-v67v9           1/1       Running      0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running      0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/elasticsearch   1         1         1            0           1m
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl logs -f elasticsearch-598ff57f45-5h7dd
Error from server (BadRequest): container "ss-elasticsearch" in pod "elasticsearch-598ff57f45-5h7dd" is waiting to start: PodInitializing
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS                  RESTARTS   AGE
pod/elasticsearch-598ff57f45-5h7dd   0/1       Init:CrashLoopBackOff   4          1m
pod/kibana-986f6847f-v67v9           1/1       Running                 0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running                 0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/elasticsearch   1         1         1            0           1m
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS                  RESTARTS   AGE
pod/elasticsearch-598ff57f45-5h7dd   0/1       Init:CrashLoopBackOff   5          4m
pod/kibana-986f6847f-v67v9           1/1       Running                 0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running                 0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/elasticsearch   1         1         1            0           4m
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl logs -f elasticsearch-598ff57f45-5h7dd
Error from server (BadRequest): container "ss-elasticsearch" in pod "elasticsearch-598ff57f45-5h7dd" is waiting to start: PodInitializing
Hungs-MBP:screening hungbang$ kompose 
.DS_Store                       backend/                        env-snippet-ss-secret.yaml      k8s-kibana/                     ss-secret-local.yaml
.env                            bitbucket-pipelines.yml         frontend/                       k8s-nginx/                      ss-secret-uat.yaml
.git/                           cloudbuild.yaml                 ingress.yaml                    k8s-redis/                      
README.md                       configs/                        k8s-backend/                    k9s-nginx/                      
apikey.txt                      docker-compose.yaml             k8s-elasticsearch/              nginx/                          
auth0/                          env-snippet-ss-secret-uat.yaml  k8s-frontend/                   simple.yaml                     
Hungs-MBP:screening hungbang$ kompose 
.DS_Store                       backend/                        env-snippet-ss-secret.yaml      k8s-kibana/                     ss-secret-local.yaml
.env                            bitbucket-pipelines.yml         frontend/                       k8s-nginx/                      ss-secret-uat.yaml
.git/                           cloudbuild.yaml                 ingress.yaml                    k8s-redis/                      
README.md                       configs/                        k8s-backend/                    k9s-nginx/                      
apikey.txt                      docker-compose.yaml             k8s-elasticsearch/              nginx/                          
auth0/                          env-snippet-ss-secret-uat.yaml  k8s-frontend/                   simple.yaml                     
Hungs-MBP:screening hungbang$ kubeval k8s-elasticsearch/elasticsearch-deployment.yaml 
The document k8s-elasticsearch/elasticsearch-deployment.yaml contains a valid Deployment
Hungs-MBP:screening hungbang$ kubectl logs -f elasticsearch-598ff57f45-5h7dd
Error from server (BadRequest): container "ss-elasticsearch" in pod "elasticsearch-598ff57f45-5h7dd" is waiting to start: PodInitializing
Hungs-MBP:screening hungbang$ kubectl get deployment
NAME            DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
elasticsearch   1         1         1            0           8m
kibana          1         1         1            1           1h
redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl delete deployment elasticsearch
deployment.extensions "elasticsearch" deleted
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS        RESTARTS   AGE
pod/elasticsearch-598ff57f45-5h7dd   0/1       Terminating   0          8m
pod/kibana-986f6847f-v67v9           1/1       Running       0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running       0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                           DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/kibana   1         1         1            1           1h
deployment.extensions/redis    1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                         READY     STATUS    RESTARTS   AGE
pod/kibana-986f6847f-v67v9   1/1       Running   0          1h
pod/redis-9dcd8d797-7khrz    1/1       Running   0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                           DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/kibana   1         1         1            1           1h
deployment.extensions/redis    1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl apply -f k8s-elasticsearch/elasticsearch-deployment.yaml 
deployment.extensions/elasticsearch created
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS     RESTARTS   AGE
pod/elasticsearch-55cd497bdf-nk7wb   0/1       Init:0/2   0          6s
pod/kibana-986f6847f-v67v9           1/1       Running    0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running    0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/elasticsearch   1         1         1            0           6s
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS     RESTARTS   AGE
pod/elasticsearch-55cd497bdf-nk7wb   0/1       Init:0/2   0          14s
pod/kibana-986f6847f-v67v9           1/1       Running    0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running    0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/elasticsearch   1         1         1            0           14s
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS    RESTARTS   AGE
pod/elasticsearch-55cd497bdf-nk7wb   1/1       Running   0          54s
pod/kibana-986f6847f-v67v9           1/1       Running   0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running   0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                         AGE
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235   9300:32235/TCP,9200:30118/TCP   1h
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107   5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>           443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48    6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/elasticsearch   1         1         1            1           54s
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ curl http://104.197.65.235:9200
{
  "name" : "LYOZfn_",
  "cluster_name" : "ss-cluster",
  "cluster_uuid" : "pNlD8atdRlOkRVcBEwdjDQ",
  "version" : {
    "number" : "5.4.3",
    "build_hash" : "eed30a8",
    "build_date" : "2017-06-22T00:34:03.743Z",
    "build_snapshot" : false,
    "lucene_version" : "6.5.1"
  },
  "tagline" : "You Know, for Search"
}
Hungs-MBP:screening hungbang$ curl http://localhost:9200/_cluster/state?pretty
{
  "cluster_name" : "ss-cluster",
  "version" : 15,
  "state_uuid" : "Fj7iudOfQ8aP4YicTxc5JQ",
  "master_node" : "wBBT-wuiScCa7Vf8cv4DYw",
  "blocks" : { },
  "nodes" : {
    "wBBT-wuiScCa7Vf8cv4DYw" : {
      "name" : "wBBT-wu",
      "ephemeral_id" : "_FtTQz0nS3GtjQ9Gmh5hXA",
      "transport_address" : "10.1.1.16:9300",
      "attributes" : {
        "ml.enabled" : "true"
      }
    }
  },
  "metadata" : {
    "cluster_uuid" : "tH_nfC72Qbe_TVk2hmHI4A",
    "templates" : {
      ".ml-notifications" : {
        "template" : ".ml-notifications",
        "order" : 0,
        "settings" : {
          "index" : {
            "number_of_shards" : "1",
            "mapper" : {
              "dynamic" : "true"
            },
            "unassigned" : {
              "node_left" : {
                "delayed_timeout" : "1m"
              }
            }
          }
        },
        "mappings" : {
          "audit_message" : {
            "properties" : {
              "level" : {
                "type" : "keyword"
              },
              "job_id" : {
                "type" : "keyword"
              },
              "node_name" : {
                "type" : "keyword"
              },
              "message" : {
                "type" : "text",
                "fields" : {
                  "raw" : {
                    "type" : "keyword"
                  }
                }
              },
              "timestamp" : {
                "type" : "date"
              }
            }
          }
        }
      },
      ".ml-meta" : {
        "template" : ".ml-meta",
        "order" : 0,
        "settings" : {
          "index" : {
            "number_of_shards" : "1",
            "mapper" : {
              "dynamic" : "true"
            },
            "unassigned" : {
              "node_left" : {
                "delayed_timeout" : "1m"
              }
            }
          }
        },
        "mappings" : { }
      },
      ".ml-state" : {
        "template" : ".ml-state",
        "order" : 0,
        "settings" : {
          "index" : {
            "translog" : {
              "durability" : "async"
            },
            "unassigned" : {
              "node_left" : {
                "delayed_timeout" : "1m"
              }
            }
          }
        },
        "mappings" : {
          "quantiles" : {
            "enabled" : false
          },
          "categorizer_state" : {
            "enabled" : false
          },
          "model_state" : {
            "enabled" : false
          }
        }
      },
      ".ml-anomalies-" : {
        "template" : ".ml-anomalies-*",
        "order" : 0,
        "settings" : {
          "index" : {
            "mapper" : {
              "dynamic" : "true"
            },
            "unassigned" : {
              "node_left" : {
                "delayed_timeout" : "1m"
              }
            },
            "translog" : {
              "durability" : "async"
            },
            "query" : {
              "default_field" : "all_field_values"
            }
          }
        },
        "mappings" : {
          "result" : {
            "properties" : {
              "record_count" : {
                "type" : "long"
              },
              "initial_anomaly_score" : {
                "type" : "double"
              },
              "raw_anomaly_score" : {
                "type" : "double"
              },
              "partition_field_name" : {
                "type" : "keyword"
              },
              "partition_field_value" : {
                "copy_to" : "all_field_values",
                "type" : "keyword"
              },
              "initial_influencer_score" : {
                "type" : "double"
              },
              "by_field_name" : {
                "type" : "keyword"
              },
              "event_count" : {
                "type" : "long"
              },
              "model_lower" : {
                "type" : "double"
              },
              "total_over_field_count" : {
                "type" : "long"
              },
              "is_interim" : {
                "type" : "boolean"
              },
              "model_median" : {
                "type" : "double"
              },
              "bucket_allocation_failures_count" : {
                "type" : "long"
              },
              "memory_status" : {
                "type" : "keyword"
              },
              "model_feature" : {
                "type" : "keyword"
              },
              "anomaly_score" : {
                "type" : "double"
              },
              "over_field_name" : {
                "type" : "keyword"
              },
              "bucket_span" : {
                "type" : "long"
              },
              "function" : {
                "type" : "keyword"
              },
              "causes" : {
                "type" : "nested",
                "properties" : {
                  "actual" : {
                    "type" : "double"
                  },
                  "partition_field_name" : {
                    "type" : "keyword"
                  },
                  "partition_field_value" : {
                    "copy_to" : "all_field_values",
                    "type" : "keyword"
                  },
                  "by_field_name" : {
                    "type" : "keyword"
                  },
                  "probability" : {
                    "type" : "double"
                  },
                  "field_name" : {
                    "type" : "keyword"
                  },
                  "by_field_value" : {
                    "copy_to" : "all_field_values",
                    "type" : "keyword"
                  },
                  "over_field_name" : {
                    "type" : "keyword"
                  },
                  "function" : {
                    "type" : "keyword"
                  },
                  "correlated_by_field_value" : {
                    "copy_to" : "all_field_values",
                    "type" : "keyword"
                  },
                  "typical" : {
                    "type" : "double"
                  },
                  "over_field_value" : {
                    "copy_to" : "all_field_values",
                    "type" : "keyword"
                  },
                  "function_description" : {
                    "type" : "keyword"
                  }
                }
              },
              "influencers" : {
                "type" : "nested",
                "properties" : {
                  "influencer_field_name" : {
                    "type" : "keyword"
                  },
                  "influencer_field_values" : {
                    "copy_to" : "all_field_values",
                    "type" : "keyword"
                  }
                }
              },
              "record_score" : {
                "type" : "double"
              },
              "all_field_values" : {
                "analyzer" : "whitespace",
                "type" : "text"
              },
              "over_field_value" : {
                "copy_to" : "all_field_values",
                "type" : "keyword"
              },
              "influencer_score" : {
                "type" : "double"
              },
              "timestamp" : {
                "type" : "date"
              },
              "partition_scores" : {
                "type" : "nested",
                "properties" : {
                  "initial_anomaly_score" : {
                    "type" : "double"
                  },
                  "partition_field_name" : {
                    "type" : "keyword"
                  },
                  "partition_field_value" : {
                    "type" : "keyword"
                  },
                  "probability" : {
                    "type" : "double"
                  }
                }
              },
              "model_upper" : {
                "type" : "double"
              },
              "result_type" : {
                "type" : "keyword"
              },
              "sequence_num" : {
                "type" : "integer"
              },
              "actual" : {
                "type" : "double"
              },
              "per_partition_max_probabilities" : {
                "type" : "nested",
                "properties" : {
                  "partition_field_value" : {
                    "type" : "keyword"
                  },
                  "max_record_score" : {
                    "type" : "double"
                  }
                }
              },
              "probability" : {
                "type" : "double"
              },
              "influencer_field_name" : {
                "type" : "keyword"
              },
              "influencer_field_value" : {
                "copy_to" : "all_field_values",
                "type" : "keyword"
              },
              "total_by_field_count" : {
                "type" : "long"
              },
              "detector_index" : {
                "type" : "integer"
              },
              "log_time" : {
                "type" : "date"
              },
              "field_name" : {
                "type" : "keyword"
              },
              "model_bytes" : {
                "type" : "long"
              },
              "processing_time_ms" : {
                "type" : "long"
              },
              "bucket_influencers" : {
                "type" : "nested",
                "properties" : {
                  "result_type" : {
                    "type" : "keyword"
                  },
                  "initial_anomaly_score" : {
                    "type" : "double"
                  },
                  "anomaly_score" : {
                    "type" : "double"
                  },
                  "sequence_num" : {
                    "type" : "integer"
                  },
                  "raw_anomaly_score" : {
                    "type" : "double"
                  },
                  "bucket_span" : {
                    "type" : "long"
                  },
                  "job_id" : {
                    "type" : "keyword"
                  },
                  "probability" : {
                    "type" : "double"
                  },
                  "influencer_field_name" : {
                    "type" : "keyword"
                  },
                  "is_interim" : {
                    "type" : "boolean"
                  },
                  "timestamp" : {
                    "type" : "date"
                  }
                }
              },
              "by_field_value" : {
                "copy_to" : "all_field_values",
                "type" : "keyword"
              },
              "initial_record_score" : {
                "type" : "double"
              },
              "job_id" : {
                "copy_to" : "all_field_values",
                "type" : "keyword"
              },
              "total_partition_field_count" : {
                "type" : "long"
              },
              "typical" : {
                "type" : "double"
              },
              "function_description" : {
                "type" : "keyword"
              }
            }
          },
          "model_snapshot" : {
            "properties" : {
              "quantiles" : {
                "enabled" : false
              },
              "latest_record_time_stamp" : {
                "type" : "date"
              },
              "snapshot_id" : {
                "type" : "keyword"
              },
              "snapshot_doc_count" : {
                "type" : "integer"
              },
              "job_id" : {
                "type" : "keyword"
              },
              "retain" : {
                "type" : "boolean"
              },
              "description" : {
                "type" : "text"
              },
              "model_size_stats" : {
                "properties" : {
                  "model_bytes" : {
                    "type" : "long"
                  },
                  "result_type" : {
                    "type" : "keyword"
                  },
                  "job_id" : {
                    "type" : "keyword"
                  },
                  "total_over_field_count" : {
                    "type" : "long"
                  },
                  "total_partition_field_count" : {
                    "type" : "long"
                  },
                  "total_by_field_count" : {
                    "type" : "long"
                  },
                  "bucket_allocation_failures_count" : {
                    "type" : "long"
                  },
                  "memory_status" : {
                    "type" : "keyword"
                  },
                  "log_time" : {
                    "type" : "date"
                  },
                  "timestamp" : {
                    "type" : "date"
                  }
                }
              },
              "latest_result_time_stamp" : {
                "type" : "date"
              },
              "timestamp" : {
                "type" : "date"
              }
            }
          },
          "data_counts" : {
            "properties" : {
              "out_of_order_timestamp_count" : {
                "type" : "long"
              },
              "empty_bucket_count" : {
                "type" : "long"
              },
              "last_data_time" : {
                "type" : "date"
              },
              "input_field_count" : {
                "type" : "long"
              },
              "invalid_date_count" : {
                "type" : "long"
              },
              "latest_record_timestamp" : {
                "type" : "date"
              },
              "missing_field_count" : {
                "type" : "long"
              },
              "latest_sparse_bucket_timestamp" : {
                "type" : "date"
              },
              "sparse_bucket_count" : {
                "type" : "long"
              },
              "bucket_count" : {
                "type" : "long"
              },
              "latest_empty_bucket_timestamp" : {
                "type" : "date"
              },
              "input_bytes" : {
                "type" : "long"
              },
              "earliest_record_timestamp" : {
                "type" : "date"
              },
              "processed_record_count" : {
                "type" : "long"
              },
              "job_id" : {
                "type" : "keyword"
              },
              "processed_field_count" : {
                "type" : "long"
              },
              "input_record_count" : {
                "type" : "long"
              }
            }
          },
          "category_definition" : {
            "properties" : {
              "regex" : {
                "type" : "keyword"
              },
              "category_id" : {
                "type" : "long"
              },
              "examples" : {
                "type" : "text"
              },
              "terms" : {
                "type" : "text"
              },
              "job_id" : {
                "type" : "keyword"
              },
              "max_matching_length" : {
                "type" : "long"
              }
            }
          }
        }
      }
    },
    "indices" : {
      ".kibana" : {
        "state" : "open",
        "settings" : {
          "index" : {
            "creation_date" : "1541054466315",
            "number_of_shards" : "1",
            "number_of_replicas" : "1",
            "uuid" : "EGzNFc7CRFW4fEukDwEWYw",
            "version" : {
              "created" : "5040399"
            },
            "provided_name" : ".kibana"
          }
        },
        "mappings" : {
          "server" : {
            "properties" : {
              "uuid" : {
                "type" : "keyword"
              }
            }
          },
          "config" : {
            "properties" : {
              "buildNum" : {
                "type" : "keyword"
              }
            }
          }
        },
        "aliases" : [ ],
        "primary_terms" : {
          "0" : 2
        },
        "in_sync_allocations" : {
          "0" : [
            "q2zkpDsUSZKsEYjsosaIhw"
          ]
        }
      },
      "ss" : {
        "state" : "open",
        "settings" : {
          "index" : {
            "refresh_interval" : "1s",
            "number_of_shards" : "5",
            "provided_name" : "ss",
            "creation_date" : "1541080992558",
            "store" : {
              "type" : "fs"
            },
            "number_of_replicas" : "1",
            "uuid" : "7taxgUpJTzmQhreJPZNcuw",
            "version" : {
              "created" : "5040399"
            }
          }
        },
        "mappings" : {
          "sanctions" : {
            "properties" : {
              "otherNames" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "ignore_above" : 256,
                    "type" : "keyword"
                  }
                }
              },
              "name" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "ignore_above" : 256,
                    "type" : "keyword"
                  }
                }
              },
              "id" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "ignore_above" : 256,
                    "type" : "keyword"
                  }
                }
              },
              "program" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "ignore_above" : 256,
                    "type" : "keyword"
                  }
                }
              },
              "source" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "ignore_above" : 256,
                    "type" : "keyword"
                  }
                }
              },
              "updatedAt" : {
                "type" : "date"
              }
            }
          },
          "users" : {
            "properties" : {
              "lastLogin" : {
                "type" : "date"
              },
              "companyId" : {
                "type" : "keyword"
              },
              "role" : {
                "fielddata" : true,
                "type" : "text"
              }
            }
          },
          "companies" : {
            "properties" : {
              "chargebeeSubscription" : {
                "type" : "nested",
                "properties" : {
                  "updatedAt" : {
                    "type" : "date"
                  }
                }
              },
              "users" : {
                "include_in_parent" : true,
                "type" : "nested",
                "properties" : {
                  "lastLogin" : {
                    "type" : "date"
                  },
                  "companyId" : {
                    "type" : "keyword"
                  },
                  "role" : {
                    "fielddata" : true,
                    "type" : "text"
                  }
                }
              }
            }
          },
          "searches" : {
            "properties" : {
              "companyId" : {
                "type" : "keyword"
              },
              "comments" : {
                "include_in_parent" : true,
                "type" : "nested",
                "properties" : {
                  "createdAt" : {
                    "type" : "date"
                  },
                  "user" : {
                    "type" : "nested",
                    "properties" : {
                      "lastLogin" : {
                        "type" : "date"
                      },
                      "companyId" : {
                        "type" : "keyword"
                      },
                      "role" : {
                        "fielddata" : true,
                        "type" : "text"
                      }
                    }
                  },
                  "updatedAt" : {
                    "type" : "date"
                  }
                }
              },
              "scannedName" : {
                "fielddata" : true,
                "type" : "text"
              },
              "documents" : {
                "include_in_parent" : true,
                "type" : "nested",
                "properties" : {
                  "updatedAt" : {
                    "type" : "date"
                  }
                }
              },
              "sanctions" : {
                "type" : "nested",
                "properties" : {
                  "otherNames" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "ignore_above" : 256,
                        "type" : "keyword"
                      }
                    }
                  },
                  "name" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "ignore_above" : 256,
                        "type" : "keyword"
                      }
                    }
                  },
                  "id" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "ignore_above" : 256,
                        "type" : "keyword"
                      }
                    }
                  },
                  "program" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "ignore_above" : 256,
                        "type" : "keyword"
                      }
                    }
                  },
                  "source" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "ignore_above" : 256,
                        "type" : "keyword"
                      }
                    }
                  },
                  "updatedAt" : {
                    "type" : "date"
                  }
                }
              },
              "user" : {
                "type" : "nested",
                "properties" : {
                  "lastLogin" : {
                    "type" : "date"
                  },
                  "companyId" : {
                    "type" : "keyword"
                  },
                  "role" : {
                    "fielddata" : true,
                    "type" : "text"
                  },
                  "name" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "ignore_above" : 256,
                        "type" : "keyword"
                      }
                    }
                  },
                  "id" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "ignore_above" : 256,
                        "type" : "keyword"
                      }
                    }
                  },
                  "email" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "ignore_above" : 256,
                        "type" : "keyword"
                      }
                    }
                  }
                }
              },
              "status" : {
                "type" : "keyword"
              },
              "updatedAt" : {
                "type" : "date"
              }
            }
          }
        },
        "aliases" : [ ],
        "primary_terms" : {
          "0" : 1,
          "1" : 1,
          "2" : 1,
          "3" : 1,
          "4" : 1
        },
        "in_sync_allocations" : {
          "1" : [
            "kbush3UXTWG4BetsMdRzYA"
          ],
          "3" : [
            "BqjLIgp8SfqHdeAXvogDfw"
          ],
          "4" : [
            "eZ_34ynyT1WKu-gn1um8Qw"
          ],
          "2" : [
            "prxjmDNXTtiNMdJZKYQw7w"
          ],
          "0" : [
            "obefqaGLRKu36VNjJOOYuw"
          ]
        }
      }
    },
    "ml" : {
      "jobs" : [ ],
      "datafeeds" : [ ]
    },
    "index-graveyard" : {
      "tombstones" : [ ]
    }
  },
  "routing_table" : {
    "indices" : {
      ".kibana" : {
        "shards" : {
          "0" : [
            {
              "state" : "STARTED",
              "primary" : true,
              "node" : "wBBT-wuiScCa7Vf8cv4DYw",
              "relocating_node" : null,
              "shard" : 0,
              "index" : ".kibana",
              "allocation_id" : {
                "id" : "q2zkpDsUSZKsEYjsosaIhw"
              }
            },
            {
              "state" : "UNASSIGNED",
              "primary" : false,
              "node" : null,
              "relocating_node" : null,
              "shard" : 0,
              "index" : ".kibana",
              "recovery_source" : {
                "type" : "PEER"
              },
              "unassigned_info" : {
                "reason" : "CLUSTER_RECOVERED",
                "at" : "2018-11-01T07:34:30.351Z",
                "delayed" : false,
                "allocation_status" : "no_attempt"
              }
            }
          ]
        }
      },
      "ss" : {
        "shards" : {
          "1" : [
            {
              "state" : "STARTED",
              "primary" : true,
              "node" : "wBBT-wuiScCa7Vf8cv4DYw",
              "relocating_node" : null,
              "shard" : 1,
              "index" : "ss",
              "allocation_id" : {
                "id" : "kbush3UXTWG4BetsMdRzYA"
              }
            },
            {
              "state" : "UNASSIGNED",
              "primary" : false,
              "node" : null,
              "relocating_node" : null,
              "shard" : 1,
              "index" : "ss",
              "recovery_source" : {
                "type" : "PEER"
              },
              "unassigned_info" : {
                "reason" : "INDEX_CREATED",
                "at" : "2018-11-01T14:03:12.847Z",
                "delayed" : false,
                "allocation_status" : "no_attempt"
              }
            }
          ],
          "3" : [
            {
              "state" : "STARTED",
              "primary" : true,
              "node" : "wBBT-wuiScCa7Vf8cv4DYw",
              "relocating_node" : null,
              "shard" : 3,
              "index" : "ss",
              "allocation_id" : {
                "id" : "BqjLIgp8SfqHdeAXvogDfw"
              }
            },
            {
              "state" : "UNASSIGNED",
              "primary" : false,
              "node" : null,
              "relocating_node" : null,
              "shard" : 3,
              "index" : "ss",
              "recovery_source" : {
                "type" : "PEER"
              },
              "unassigned_info" : {
                "reason" : "INDEX_CREATED",
                "at" : "2018-11-01T14:03:12.847Z",
                "delayed" : false,
                "allocation_status" : "no_attempt"
              }
            }
          ],
          "4" : [
            {
              "state" : "STARTED",
              "primary" : true,
              "node" : "wBBT-wuiScCa7Vf8cv4DYw",
              "relocating_node" : null,
              "shard" : 4,
              "index" : "ss",
              "allocation_id" : {
                "id" : "eZ_34ynyT1WKu-gn1um8Qw"
              }
            },
            {
              "state" : "UNASSIGNED",
              "primary" : false,
              "node" : null,
              "relocating_node" : null,
              "shard" : 4,
              "index" : "ss",
              "recovery_source" : {
                "type" : "PEER"
              },
              "unassigned_info" : {
                "reason" : "INDEX_CREATED",
                "at" : "2018-11-01T14:03:12.847Z",
                "delayed" : false,
                "allocation_status" : "no_attempt"
              }
            }
          ],
          "2" : [
            {
              "state" : "STARTED",
              "primary" : true,
              "node" : "wBBT-wuiScCa7Vf8cv4DYw",
              "relocating_node" : null,
              "shard" : 2,
              "index" : "ss",
              "allocation_id" : {
                "id" : "prxjmDNXTtiNMdJZKYQw7w"
              }
            },
            {
              "state" : "UNASSIGNED",
              "primary" : false,
              "node" : null,
              "relocating_node" : null,
              "shard" : 2,
              "index" : "ss",
              "recovery_source" : {
                "type" : "PEER"
              },
              "unassigned_info" : {
                "reason" : "INDEX_CREATED",
                "at" : "2018-11-01T14:03:12.847Z",
                "delayed" : false,
                "allocation_status" : "no_attempt"
              }
            }
          ],
          "0" : [
            {
              "state" : "STARTED",
              "primary" : true,
              "node" : "wBBT-wuiScCa7Vf8cv4DYw",
              "relocating_node" : null,
              "shard" : 0,
              "index" : "ss",
              "allocation_id" : {
                "id" : "obefqaGLRKu36VNjJOOYuw"
              }
            },
            {
              "state" : "UNASSIGNED",
              "primary" : false,
              "node" : null,
              "relocating_node" : null,
              "shard" : 0,
              "index" : "ss",
              "recovery_source" : {
                "type" : "PEER"
              },
              "unassigned_info" : {
                "reason" : "INDEX_CREATED",
                "at" : "2018-11-01T14:03:12.847Z",
                "delayed" : false,
                "allocation_status" : "no_attempt"
              }
            }
          ]
        }
      }
    }
  },
  "routing_nodes" : {
    "unassigned" : [
      {
        "state" : "UNASSIGNED",
        "primary" : false,
        "node" : null,
        "relocating_node" : null,
        "shard" : 0,
        "index" : ".kibana",
        "recovery_source" : {
          "type" : "PEER"
        },
        "unassigned_info" : {
          "reason" : "CLUSTER_RECOVERED",
          "at" : "2018-11-01T07:34:30.351Z",
          "delayed" : false,
          "allocation_status" : "no_attempt"
        }
      },
      {
        "state" : "UNASSIGNED",
        "primary" : false,
        "node" : null,
        "relocating_node" : null,
        "shard" : 1,
        "index" : "ss",
        "recovery_source" : {
          "type" : "PEER"
        },
        "unassigned_info" : {
          "reason" : "INDEX_CREATED",
          "at" : "2018-11-01T14:03:12.847Z",
          "delayed" : false,
          "allocation_status" : "no_attempt"
        }
      },
      {
        "state" : "UNASSIGNED",
        "primary" : false,
        "node" : null,
        "relocating_node" : null,
        "shard" : 3,
        "index" : "ss",
        "recovery_source" : {
          "type" : "PEER"
        },
        "unassigned_info" : {
          "reason" : "INDEX_CREATED",
          "at" : "2018-11-01T14:03:12.847Z",
          "delayed" : false,
          "allocation_status" : "no_attempt"
        }
      },
      {
        "state" : "UNASSIGNED",
        "primary" : false,
        "node" : null,
        "relocating_node" : null,
        "shard" : 4,
        "index" : "ss",
        "recovery_source" : {
          "type" : "PEER"
        },
        "unassigned_info" : {
          "reason" : "INDEX_CREATED",
          "at" : "2018-11-01T14:03:12.847Z",
          "delayed" : false,
          "allocation_status" : "no_attempt"
        }
      },
      {
        "state" : "UNASSIGNED",
        "primary" : false,
        "node" : null,
        "relocating_node" : null,
        "shard" : 2,
        "index" : "ss",
        "recovery_source" : {
          "type" : "PEER"
        },
        "unassigned_info" : {
          "reason" : "INDEX_CREATED",
          "at" : "2018-11-01T14:03:12.847Z",
          "delayed" : false,
          "allocation_status" : "no_attempt"
        }
      },
      {
        "state" : "UNASSIGNED",
        "primary" : false,
        "node" : null,
        "relocating_node" : null,
        "shard" : 0,
        "index" : "ss",
        "recovery_source" : {
          "type" : "PEER"
        },
        "unassigned_info" : {
          "reason" : "INDEX_CREATED",
          "at" : "2018-11-01T14:03:12.847Z",
          "delayed" : false,
          "allocation_status" : "no_attempt"
        }
      }
    ],
    "nodes" : {
      "wBBT-wuiScCa7Vf8cv4DYw" : [
        {
          "state" : "STARTED",
          "primary" : true,
          "node" : "wBBT-wuiScCa7Vf8cv4DYw",
          "relocating_node" : null,
          "shard" : 0,
          "index" : ".kibana",
          "allocation_id" : {
            "id" : "q2zkpDsUSZKsEYjsosaIhw"
          }
        },
        {
          "state" : "STARTED",
          "primary" : true,
          "node" : "wBBT-wuiScCa7Vf8cv4DYw",
          "relocating_node" : null,
          "shard" : 1,
          "index" : "ss",
          "allocation_id" : {
            "id" : "kbush3UXTWG4BetsMdRzYA"
          }
        },
        {
          "state" : "STARTED",
          "primary" : true,
          "node" : "wBBT-wuiScCa7Vf8cv4DYw",
          "relocating_node" : null,
          "shard" : 3,
          "index" : "ss",
          "allocation_id" : {
            "id" : "BqjLIgp8SfqHdeAXvogDfw"
          }
        },
        {
          "state" : "STARTED",
          "primary" : true,
          "node" : "wBBT-wuiScCa7Vf8cv4DYw",
          "relocating_node" : null,
          "shard" : 4,
          "index" : "ss",
          "allocation_id" : {
            "id" : "eZ_34ynyT1WKu-gn1um8Qw"
          }
        },
        {
          "state" : "STARTED",
          "primary" : true,
          "node" : "wBBT-wuiScCa7Vf8cv4DYw",
          "relocating_node" : null,
          "shard" : 2,
          "index" : "ss",
          "allocation_id" : {
            "id" : "prxjmDNXTtiNMdJZKYQw7w"
          }
        },
        {
          "state" : "STARTED",
          "primary" : true,
          "node" : "wBBT-wuiScCa7Vf8cv4DYw",
          "relocating_node" : null,
          "shard" : 0,
          "index" : "ss",
          "allocation_id" : {
            "id" : "obefqaGLRKu36VNjJOOYuw"
          }
        }
      ]
    }
  }
}
Hungs-MBP:screening hungbang$ curl http://104.197.65.235:9200
{
  "name" : "LYOZfn_",
  "cluster_name" : "ss-cluster",
  "cluster_uuid" : "pNlD8atdRlOkRVcBEwdjDQ",
  "version" : {
    "number" : "5.4.3",
    "build_hash" : "eed30a8",
    "build_date" : "2017-06-22T00:34:03.743Z",
    "build_snapshot" : false,
    "lucene_version" : "6.5.1"
  },
  "tagline" : "You Know, for Search"
}
Hungs-MBP:screening hungbang$ curl http://104.197.65.235:9200/_cluster/state?pretty
{
  "cluster_name" : "ss-cluster",
  "version" : 10,
  "state_uuid" : "UhtoqmaMRJa3CYOVPGp9qA",
  "master_node" : "LYOZfn_GQ7iYii8nUiK1HA",
  "blocks" : { },
  "nodes" : {
    "LYOZfn_GQ7iYii8nUiK1HA" : {
      "name" : "LYOZfn_",
      "ephemeral_id" : "MC7SFiLYTnqUcB_dnR1iVg",
      "transport_address" : "10.20.1.8:9300",
      "attributes" : {
        "ml.enabled" : "true"
      }
    }
  },
  "metadata" : {
    "cluster_uuid" : "pNlD8atdRlOkRVcBEwdjDQ",
    "templates" : {
      ".ml-anomalies-" : {
        "template" : ".ml-anomalies-*",
        "order" : 0,
        "settings" : {
          "index" : {
            "mapper" : {
              "dynamic" : "true"
            },
            "unassigned" : {
              "node_left" : {
                "delayed_timeout" : "1m"
              }
            },
            "translog" : {
              "durability" : "async"
            },
            "query" : {
              "default_field" : "all_field_values"
            }
          }
        },
        "mappings" : {
          "category_definition" : {
            "properties" : {
              "regex" : {
                "type" : "keyword"
              },
              "category_id" : {
                "type" : "long"
              },
              "examples" : {
                "type" : "text"
              },
              "terms" : {
                "type" : "text"
              },
              "job_id" : {
                "type" : "keyword"
              },
              "max_matching_length" : {
                "type" : "long"
              }
            }
          },
          "model_snapshot" : {
            "properties" : {
              "quantiles" : {
                "enabled" : false
              },
              "latest_record_time_stamp" : {
                "type" : "date"
              },
              "snapshot_id" : {
                "type" : "keyword"
              },
              "snapshot_doc_count" : {
                "type" : "integer"
              },
              "job_id" : {
                "type" : "keyword"
              },
              "retain" : {
                "type" : "boolean"
              },
              "description" : {
                "type" : "text"
              },
              "model_size_stats" : {
                "properties" : {
                  "model_bytes" : {
                    "type" : "long"
                  },
                  "result_type" : {
                    "type" : "keyword"
                  },
                  "job_id" : {
                    "type" : "keyword"
                  },
                  "total_over_field_count" : {
                    "type" : "long"
                  },
                  "total_partition_field_count" : {
                    "type" : "long"
                  },
                  "total_by_field_count" : {
                    "type" : "long"
                  },
                  "bucket_allocation_failures_count" : {
                    "type" : "long"
                  },
                  "memory_status" : {
                    "type" : "keyword"
                  },
                  "log_time" : {
                    "type" : "date"
                  },
                  "timestamp" : {
                    "type" : "date"
                  }
                }
              },
              "latest_result_time_stamp" : {
                "type" : "date"
              },
              "timestamp" : {
                "type" : "date"
              }
            }
          },
          "result" : {
            "properties" : {
              "record_count" : {
                "type" : "long"
              },
              "initial_anomaly_score" : {
                "type" : "double"
              },
              "raw_anomaly_score" : {
                "type" : "double"
              },
              "partition_field_name" : {
                "type" : "keyword"
              },
              "partition_field_value" : {
                "copy_to" : "all_field_values",
                "type" : "keyword"
              },
              "initial_influencer_score" : {
                "type" : "double"
              },
              "by_field_name" : {
                "type" : "keyword"
              },
              "event_count" : {
                "type" : "long"
              },
              "model_lower" : {
                "type" : "double"
              },
              "total_over_field_count" : {
                "type" : "long"
              },
              "is_interim" : {
                "type" : "boolean"
              },
              "model_median" : {
                "type" : "double"
              },
              "bucket_allocation_failures_count" : {
                "type" : "long"
              },
              "memory_status" : {
                "type" : "keyword"
              },
              "model_feature" : {
                "type" : "keyword"
              },
              "anomaly_score" : {
                "type" : "double"
              },
              "over_field_name" : {
                "type" : "keyword"
              },
              "bucket_span" : {
                "type" : "long"
              },
              "function" : {
                "type" : "keyword"
              },
              "causes" : {
                "type" : "nested",
                "properties" : {
                  "actual" : {
                    "type" : "double"
                  },
                  "partition_field_name" : {
                    "type" : "keyword"
                  },
                  "partition_field_value" : {
                    "copy_to" : "all_field_values",
                    "type" : "keyword"
                  },
                  "by_field_name" : {
                    "type" : "keyword"
                  },
                  "probability" : {
                    "type" : "double"
                  },
                  "field_name" : {
                    "type" : "keyword"
                  },
                  "by_field_value" : {
                    "copy_to" : "all_field_values",
                    "type" : "keyword"
                  },
                  "over_field_name" : {
                    "type" : "keyword"
                  },
                  "function" : {
                    "type" : "keyword"
                  },
                  "correlated_by_field_value" : {
                    "copy_to" : "all_field_values",
                    "type" : "keyword"
                  },
                  "typical" : {
                    "type" : "double"
                  },
                  "over_field_value" : {
                    "copy_to" : "all_field_values",
                    "type" : "keyword"
                  },
                  "function_description" : {
                    "type" : "keyword"
                  }
                }
              },
              "influencers" : {
                "type" : "nested",
                "properties" : {
                  "influencer_field_name" : {
                    "type" : "keyword"
                  },
                  "influencer_field_values" : {
                    "copy_to" : "all_field_values",
                    "type" : "keyword"
                  }
                }
              },
              "record_score" : {
                "type" : "double"
              },
              "all_field_values" : {
                "analyzer" : "whitespace",
                "type" : "text"
              },
              "over_field_value" : {
                "copy_to" : "all_field_values",
                "type" : "keyword"
              },
              "influencer_score" : {
                "type" : "double"
              },
              "timestamp" : {
                "type" : "date"
              },
              "partition_scores" : {
                "type" : "nested",
                "properties" : {
                  "initial_anomaly_score" : {
                    "type" : "double"
                  },
                  "partition_field_name" : {
                    "type" : "keyword"
                  },
                  "partition_field_value" : {
                    "type" : "keyword"
                  },
                  "probability" : {
                    "type" : "double"
                  }
                }
              },
              "model_upper" : {
                "type" : "double"
              },
              "result_type" : {
                "type" : "keyword"
              },
              "sequence_num" : {
                "type" : "integer"
              },
              "actual" : {
                "type" : "double"
              },
              "per_partition_max_probabilities" : {
                "type" : "nested",
                "properties" : {
                  "partition_field_value" : {
                    "type" : "keyword"
                  },
                  "max_record_score" : {
                    "type" : "double"
                  }
                }
              },
              "probability" : {
                "type" : "double"
              },
              "influencer_field_name" : {
                "type" : "keyword"
              },
              "influencer_field_value" : {
                "copy_to" : "all_field_values",
                "type" : "keyword"
              },
              "total_by_field_count" : {
                "type" : "long"
              },
              "detector_index" : {
                "type" : "integer"
              },
              "log_time" : {
                "type" : "date"
              },
              "field_name" : {
                "type" : "keyword"
              },
              "model_bytes" : {
                "type" : "long"
              },
              "processing_time_ms" : {
                "type" : "long"
              },
              "bucket_influencers" : {
                "type" : "nested",
                "properties" : {
                  "result_type" : {
                    "type" : "keyword"
                  },
                  "initial_anomaly_score" : {
                    "type" : "double"
                  },
                  "anomaly_score" : {
                    "type" : "double"
                  },
                  "sequence_num" : {
                    "type" : "integer"
                  },
                  "raw_anomaly_score" : {
                    "type" : "double"
                  },
                  "bucket_span" : {
                    "type" : "long"
                  },
                  "job_id" : {
                    "type" : "keyword"
                  },
                  "probability" : {
                    "type" : "double"
                  },
                  "influencer_field_name" : {
                    "type" : "keyword"
                  },
                  "is_interim" : {
                    "type" : "boolean"
                  },
                  "timestamp" : {
                    "type" : "date"
                  }
                }
              },
              "by_field_value" : {
                "copy_to" : "all_field_values",
                "type" : "keyword"
              },
              "initial_record_score" : {
                "type" : "double"
              },
              "job_id" : {
                "copy_to" : "all_field_values",
                "type" : "keyword"
              },
              "total_partition_field_count" : {
                "type" : "long"
              },
              "typical" : {
                "type" : "double"
              },
              "function_description" : {
                "type" : "keyword"
              }
            }
          },
          "data_counts" : {
            "properties" : {
              "out_of_order_timestamp_count" : {
                "type" : "long"
              },
              "empty_bucket_count" : {
                "type" : "long"
              },
              "last_data_time" : {
                "type" : "date"
              },
              "input_field_count" : {
                "type" : "long"
              },
              "invalid_date_count" : {
                "type" : "long"
              },
              "latest_record_timestamp" : {
                "type" : "date"
              },
              "missing_field_count" : {
                "type" : "long"
              },
              "latest_sparse_bucket_timestamp" : {
                "type" : "date"
              },
              "sparse_bucket_count" : {
                "type" : "long"
              },
              "bucket_count" : {
                "type" : "long"
              },
              "latest_empty_bucket_timestamp" : {
                "type" : "date"
              },
              "input_bytes" : {
                "type" : "long"
              },
              "earliest_record_timestamp" : {
                "type" : "date"
              },
              "processed_record_count" : {
                "type" : "long"
              },
              "job_id" : {
                "type" : "keyword"
              },
              "processed_field_count" : {
                "type" : "long"
              },
              "input_record_count" : {
                "type" : "long"
              }
            }
          }
        }
      },
      ".ml-state" : {
        "template" : ".ml-state",
        "order" : 0,
        "settings" : {
          "index" : {
            "translog" : {
              "durability" : "async"
            },
            "unassigned" : {
              "node_left" : {
                "delayed_timeout" : "1m"
              }
            }
          }
        },
        "mappings" : {
          "quantiles" : {
            "enabled" : false
          },
          "model_state" : {
            "enabled" : false
          },
          "categorizer_state" : {
            "enabled" : false
          }
        }
      },
      ".ml-meta" : {
        "template" : ".ml-meta",
        "order" : 0,
        "settings" : {
          "index" : {
            "number_of_shards" : "1",
            "mapper" : {
              "dynamic" : "true"
            },
            "unassigned" : {
              "node_left" : {
                "delayed_timeout" : "1m"
              }
            }
          }
        },
        "mappings" : { }
      },
      ".ml-notifications" : {
        "template" : ".ml-notifications",
        "order" : 0,
        "settings" : {
          "index" : {
            "number_of_shards" : "1",
            "mapper" : {
              "dynamic" : "true"
            },
            "unassigned" : {
              "node_left" : {
                "delayed_timeout" : "1m"
              }
            }
          }
        },
        "mappings" : {
          "audit_message" : {
            "properties" : {
              "level" : {
                "type" : "keyword"
              },
              "job_id" : {
                "type" : "keyword"
              },
              "node_name" : {
                "type" : "keyword"
              },
              "message" : {
                "type" : "text",
                "fields" : {
                  "raw" : {
                    "type" : "keyword"
                  }
                }
              },
              "timestamp" : {
                "type" : "date"
              }
            }
          }
        }
      }
    },
    "indices" : {
      ".kibana" : {
        "state" : "open",
        "settings" : {
          "index" : {
            "creation_date" : "1541090991259",
            "number_of_shards" : "1",
            "number_of_replicas" : "1",
            "uuid" : "OAanVSiCSaOnLrSKcC76FQ",
            "version" : {
              "created" : "5040399"
            },
            "provided_name" : ".kibana"
          }
        },
        "mappings" : {
          "server" : {
            "properties" : {
              "uuid" : {
                "type" : "keyword"
              }
            }
          },
          "config" : {
            "properties" : {
              "buildNum" : {
                "type" : "keyword"
              }
            }
          }
        },
        "aliases" : [ ],
        "primary_terms" : {
          "0" : 1
        },
        "in_sync_allocations" : {
          "0" : [
            "M0eYgUG9TZud_n1zKZdmTA"
          ]
        }
      }
    },
    "index-graveyard" : {
      "tombstones" : [ ]
    },
    "ml" : {
      "jobs" : [ ],
      "datafeeds" : [ ]
    }
  },
  "routing_table" : {
    "indices" : {
      ".kibana" : {
        "shards" : {
          "0" : [
            {
              "state" : "STARTED",
              "primary" : true,
              "node" : "LYOZfn_GQ7iYii8nUiK1HA",
              "relocating_node" : null,
              "shard" : 0,
              "index" : ".kibana",
              "allocation_id" : {
                "id" : "M0eYgUG9TZud_n1zKZdmTA"
              }
            },
            {
              "state" : "UNASSIGNED",
              "primary" : false,
              "node" : null,
              "relocating_node" : null,
              "shard" : 0,
              "index" : ".kibana",
              "recovery_source" : {
                "type" : "PEER"
              },
              "unassigned_info" : {
                "reason" : "INDEX_CREATED",
                "at" : "2018-11-01T16:49:51.351Z",
                "delayed" : false,
                "allocation_status" : "no_attempt"
              }
            }
          ]
        }
      }
    }
  },
  "routing_nodes" : {
    "unassigned" : [
      {
        "state" : "UNASSIGNED",
        "primary" : false,
        "node" : null,
        "relocating_node" : null,
        "shard" : 0,
        "index" : ".kibana",
        "recovery_source" : {
          "type" : "PEER"
        },
        "unassigned_info" : {
          "reason" : "INDEX_CREATED",
          "at" : "2018-11-01T16:49:51.351Z",
          "delayed" : false,
          "allocation_status" : "no_attempt"
        }
      }
    ],
    "nodes" : {
      "LYOZfn_GQ7iYii8nUiK1HA" : [
        {
          "state" : "STARTED",
          "primary" : true,
          "node" : "LYOZfn_GQ7iYii8nUiK1HA",
          "relocating_node" : null,
          "shard" : 0,
          "index" : ".kibana",
          "allocation_id" : {
            "id" : "M0eYgUG9TZud_n1zKZdmTA"
          }
        }
      ]
    }
  }
}
Hungs-MBP:screening hungbang$ kubectl apply -f k8s-backend/,k8s-frontend/
persistentvolumeclaim/backend-claim0 created
deployment.extensions/backend created
service/backend created
deployment.extensions/frontend created
service/frontend created
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS             RESTARTS   AGE
pod/backend-58cdf6cd6b-rqzpw         0/1       ImagePullBackOff   0          44s
pod/elasticsearch-55cd497bdf-nk7wb   1/1       Running            0          5m
pod/frontend-8677d4db47-vsf7p        0/1       ImagePullBackOff   0          43s
pod/kibana-986f6847f-v67v9           1/1       Running            0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running            0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)                         AGE
service/backend         LoadBalancer   10.23.244.73    104.198.150.214   8080:31386/TCP,8000:31447/TCP   43s
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235    9300:32235/TCP,9200:30118/TCP   1h
service/frontend        LoadBalancer   10.23.244.47    <pending>         4200:30752/TCP                  42s
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107    5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>            443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48     6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/backend         1         1         1            0           44s
deployment.extensions/elasticsearch   1         1         1            1           5m
deployment.extensions/frontend        1         1         1            0           43s
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl describe backend-58cdf6cd6b-rqzpw
error: the server doesn't have a resource type "backend-58cdf6cd6b-rqzpw"
Hungs-MBP:screening hungbang$ kubectl describe pod  backend-58cdf6cd6b-rqzpw
Name:           backend-58cdf6cd6b-rqzpw
Namespace:      default
Node:           gke-cloud-build-screenin-default-pool-d23c46b8-2hm7/10.128.0.3
Start Time:     Thu, 01 Nov 2018 23:54:14 +0700
Labels:         io.kompose.service=backend
                pod-template-hash=1478927826
Annotations:    kubernetes.io/limit-ranger=LimitRanger plugin set: cpu request for container ss-backend
Status:         Pending
IP:             10.20.1.9
Controlled By:  ReplicaSet/backend-58cdf6cd6b
Containers:
  ss-backend:
    Container ID:   
    Image:          gcr.io/sanctionscreen/ss-backend
    Image ID:       
    Ports:          8080/TCP, 8000/TCP
    Host Ports:     0/TCP, 0/TCP
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:  100m
    Environment:
      ES_JAVA_OPTS:                    -Xms1g -Xmx3g
      CHARGEBEE_API_KEY:               <set to the key 'chargebee-api-key' in secret 'ss-secret'>               Optional: false
      CHARGEBEE_SITE:                  <set to the key 'chargebee-site' in secret 'ss-secret'>                  Optional: false
      CHARGEBEE_DEFAULT_PLAN:          <set to the key 'chargebee-default-plan' in secret 'ss-secret'>          Optional: false
      AUTH0_DOMAIN:                    <set to the key 'auth0-domain' in secret 'ss-secret'>                    Optional: false
      AUTH0_ISSUER:                    <set to the key 'auth0-issuer' in secret 'ss-secret'>                    Optional: false
      AUTH0_CLIENT_ID:                 <set to the key 'auth0-client-id' in secret 'ss-secret'>                 Optional: false
      AUTH0_API_AUDIENCE:              <set to the key 'auth0-api-audience' in secret 'ss-secret'>              Optional: false
      AUTH0_API_TOKEN:                 <set to the key 'auth0-api-token' in secret 'ss-secret'>                 Optional: false
      GOOGLE_APPLICATION_CREDENTIALS:  <set to the key 'google-application-credentials' in secret 'ss-secret'>  Optional: false
      GCP_PROJECT_ID:                  <set to the key 'gcp-project-id' in secret 'ss-secret'>                  Optional: false
      GSC_BUCKET_ID:                   <set to the key 'gsc-bucket-id' in secret 'ss-secret'>                   Optional: false
    Mounts:
      /opt/ss-config from ss-gce-access (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
Conditions:
  Type           Status
  Initialized    True 
  Ready          False 
  PodScheduled   True 
Volumes:
  ss-gce-access:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  ss-gcs-access
    Optional:    false
  default-token-4kxcq:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-4kxcq
    Optional:    false
QoS Class:       Burstable
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age               From                                                          Message
  ----     ------                 ----              ----                                                          -------
  Normal   Scheduled              1m                default-scheduler                                             Successfully assigned backend-58cdf6cd6b-rqzpw to gke-cloud-build-screenin-default-pool-d23c46b8-2hm7
  Normal   SuccessfulMountVolume  1m                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "ss-gce-access"
  Normal   SuccessfulMountVolume  1m                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "default-token-4kxcq"
  Normal   Pulling                37s (x3 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  pulling image "gcr.io/sanctionscreen/ss-backend"
  Warning  Failed                 36s (x3 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Failed to pull image "gcr.io/sanctionscreen/ss-backend": rpc error: code = Unknown desc = Error: Status 405 trying to pull repository sanctionscreen/ss-backend: "v1 Registry API is disabled. If you are not explicitly using the v1 Registry API, it is possible your v2 image could not be found. Verify that your image is available, or retry with `dockerd --disable-legacy-registry`. See https://cloud.google.com/container-registry/docs/support/deprecation-notices"
  Warning  Failed                 36s (x3 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Error: ErrImagePull
  Normal   BackOff                10s (x4 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Back-off pulling image "gcr.io/sanctionscreen/ss-backend"
  Warning  Failed                 10s (x4 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Error: ImagePullBackOff
Hungs-MBP:screening hungbang$ gcloud auth configure-docker 
gcloud credential helpers already registered correctly.
Hungs-MBP:screening hungbang$ kubectl describe pod  backend-58cdf6cd6b-rqzpw
Name:           backend-58cdf6cd6b-rqzpw
Namespace:      default
Node:           gke-cloud-build-screenin-default-pool-d23c46b8-2hm7/10.128.0.3
Start Time:     Thu, 01 Nov 2018 23:54:14 +0700
Labels:         io.kompose.service=backend
                pod-template-hash=1478927826
Annotations:    kubernetes.io/limit-ranger=LimitRanger plugin set: cpu request for container ss-backend
Status:         Pending
IP:             10.20.1.9
Controlled By:  ReplicaSet/backend-58cdf6cd6b
Containers:
  ss-backend:
    Container ID:   
    Image:          gcr.io/sanctionscreen/ss-backend
    Image ID:       
    Ports:          8080/TCP, 8000/TCP
    Host Ports:     0/TCP, 0/TCP
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:  100m
    Environment:
      ES_JAVA_OPTS:                    -Xms1g -Xmx3g
      CHARGEBEE_API_KEY:               <set to the key 'chargebee-api-key' in secret 'ss-secret'>               Optional: false
      CHARGEBEE_SITE:                  <set to the key 'chargebee-site' in secret 'ss-secret'>                  Optional: false
      CHARGEBEE_DEFAULT_PLAN:          <set to the key 'chargebee-default-plan' in secret 'ss-secret'>          Optional: false
      AUTH0_DOMAIN:                    <set to the key 'auth0-domain' in secret 'ss-secret'>                    Optional: false
      AUTH0_ISSUER:                    <set to the key 'auth0-issuer' in secret 'ss-secret'>                    Optional: false
      AUTH0_CLIENT_ID:                 <set to the key 'auth0-client-id' in secret 'ss-secret'>                 Optional: false
      AUTH0_API_AUDIENCE:              <set to the key 'auth0-api-audience' in secret 'ss-secret'>              Optional: false
      AUTH0_API_TOKEN:                 <set to the key 'auth0-api-token' in secret 'ss-secret'>                 Optional: false
      GOOGLE_APPLICATION_CREDENTIALS:  <set to the key 'google-application-credentials' in secret 'ss-secret'>  Optional: false
      GCP_PROJECT_ID:                  <set to the key 'gcp-project-id' in secret 'ss-secret'>                  Optional: false
      GSC_BUCKET_ID:                   <set to the key 'gsc-bucket-id' in secret 'ss-secret'>                   Optional: false
    Mounts:
      /opt/ss-config from ss-gce-access (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
Conditions:
  Type           Status
  Initialized    True 
  Ready          False 
  PodScheduled   True 
Volumes:
  ss-gce-access:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  ss-gcs-access
    Optional:    false
  default-token-4kxcq:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-4kxcq
    Optional:    false
QoS Class:       Burstable
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age              From                                                          Message
  ----     ------                 ----             ----                                                          -------
  Normal   Scheduled              3m               default-scheduler                                             Successfully assigned backend-58cdf6cd6b-rqzpw to gke-cloud-build-screenin-default-pool-d23c46b8-2hm7
  Normal   SuccessfulMountVolume  3m               kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "ss-gce-access"
  Normal   SuccessfulMountVolume  3m               kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "default-token-4kxcq"
  Normal   Pulling                2m (x4 over 3m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  pulling image "gcr.io/sanctionscreen/ss-backend"
  Warning  Failed                 2m (x4 over 3m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Failed to pull image "gcr.io/sanctionscreen/ss-backend": rpc error: code = Unknown desc = Error: Status 405 trying to pull repository sanctionscreen/ss-backend: "v1 Registry API is disabled. If you are not explicitly using the v1 Registry API, it is possible your v2 image could not be found. Verify that your image is available, or retry with `dockerd --disable-legacy-registry`. See https://cloud.google.com/container-registry/docs/support/deprecation-notices"
  Warning  Failed                 2m (x4 over 3m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Error: ErrImagePull
  Normal   BackOff                2m (x5 over 3m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Back-off pulling image "gcr.io/sanctionscreen/ss-backend"
  Warning  Failed                 2m (x6 over 3m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Error: ImagePullBackOff
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS             RESTARTS   AGE
pod/backend-58cdf6cd6b-rqzpw         0/1       ImagePullBackOff   0          11m
pod/elasticsearch-55cd497bdf-nk7wb   1/1       Running            0          16m
pod/frontend-8677d4db47-vsf7p        0/1       ImagePullBackOff   0          11m
pod/kibana-986f6847f-v67v9           1/1       Running            0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running            0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)                         AGE
service/backend         LoadBalancer   10.23.244.73    104.198.150.214   8080:31386/TCP,8000:31447/TCP   11m
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235    9300:32235/TCP,9200:30118/TCP   1h
service/frontend        LoadBalancer   10.23.244.47    35.193.50.159     4200:30752/TCP                  11m
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107    5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>            443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48     6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/backend         1         1         1            0           11m
deployment.extensions/elasticsearch   1         1         1            1           16m
deployment.extensions/frontend        1         1         1            0           11m
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl delete pod backend
Error from server (NotFound): pods "backend" not found
Hungs-MBP:screening hungbang$ kubectl delete deployment backend
deployment.extensions "backend" deleted
Hungs-MBP:screening hungbang$ kubectl delete deployment frontend
deployment.extensions "frontend" deleted
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS    RESTARTS   AGE
pod/elasticsearch-55cd497bdf-nk7wb   1/1       Running   0          17m
pod/kibana-986f6847f-v67v9           1/1       Running   0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running   0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)                         AGE
service/backend         LoadBalancer   10.23.244.73    104.198.150.214   8080:31386/TCP,8000:31447/TCP   12m
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235    9300:32235/TCP,9200:30118/TCP   1h
service/frontend        LoadBalancer   10.23.244.47    35.193.50.159     4200:30752/TCP                  12m
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107    5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>            443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48     6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/elasticsearch   1         1         1            1           17m
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl apply -f k8s-backend/,k8s-frontend/
persistentvolumeclaim/backend-claim0 configured
deployment.extensions/backend created
service/backend configured
deployment.extensions/frontend created
service/frontend configured
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS             RESTARTS   AGE
pod/backend-58cdf6cd6b-rs2rs         0/1       ImagePullBackOff   0          6s
pod/elasticsearch-55cd497bdf-nk7wb   1/1       Running            0          18m
pod/frontend-8677d4db47-lld5m        0/1       ErrImagePull       0          5s
pod/kibana-986f6847f-v67v9           1/1       Running            0          1h
pod/redis-9dcd8d797-7khrz            1/1       Running            0          1h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)                         AGE
service/backend         LoadBalancer   10.23.244.73    104.198.150.214   8080:31386/TCP,8000:31447/TCP   13m
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235    9300:32235/TCP,9200:30118/TCP   1h
service/frontend        LoadBalancer   10.23.244.47    35.193.50.159     4200:30752/TCP                  13m
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107    5601:31472/TCP                  1h
service/kubernetes      ClusterIP      10.23.240.1     <none>            443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48     6379:31018/TCP                  1h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/backend         1         1         1            0           6s
deployment.extensions/elasticsearch   1         1         1            1           18m
deployment.extensions/frontend        1         1         1            0           5s
deployment.extensions/kibana          1         1         1            1           1h
deployment.extensions/redis           1         1         1            1           1h
Hungs-MBP:screening hungbang$ kubectl describe pod backend-58cdf6cd6b-rs2rs
Name:           backend-58cdf6cd6b-rs2rs
Namespace:      default
Node:           gke-cloud-build-screenin-default-pool-d23c46b8-2hm7/10.128.0.3
Start Time:     Fri, 02 Nov 2018 00:07:15 +0700
Labels:         io.kompose.service=backend
                pod-template-hash=1478927826
Annotations:    kubernetes.io/limit-ranger=LimitRanger plugin set: cpu request for container ss-backend
Status:         Pending
IP:             10.20.1.20
Controlled By:  ReplicaSet/backend-58cdf6cd6b
Containers:
  ss-backend:
    Container ID:   
    Image:          gcr.io/sanctionscreen/ss-backend
    Image ID:       
    Ports:          8080/TCP, 8000/TCP
    Host Ports:     0/TCP, 0/TCP
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:  100m
    Environment:
      ES_JAVA_OPTS:                    -Xms1g -Xmx3g
      CHARGEBEE_API_KEY:               <set to the key 'chargebee-api-key' in secret 'ss-secret'>               Optional: false
      CHARGEBEE_SITE:                  <set to the key 'chargebee-site' in secret 'ss-secret'>                  Optional: false
      CHARGEBEE_DEFAULT_PLAN:          <set to the key 'chargebee-default-plan' in secret 'ss-secret'>          Optional: false
      AUTH0_DOMAIN:                    <set to the key 'auth0-domain' in secret 'ss-secret'>                    Optional: false
      AUTH0_ISSUER:                    <set to the key 'auth0-issuer' in secret 'ss-secret'>                    Optional: false
      AUTH0_CLIENT_ID:                 <set to the key 'auth0-client-id' in secret 'ss-secret'>                 Optional: false
      AUTH0_API_AUDIENCE:              <set to the key 'auth0-api-audience' in secret 'ss-secret'>              Optional: false
      AUTH0_API_TOKEN:                 <set to the key 'auth0-api-token' in secret 'ss-secret'>                 Optional: false
      GOOGLE_APPLICATION_CREDENTIALS:  <set to the key 'google-application-credentials' in secret 'ss-secret'>  Optional: false
      GCP_PROJECT_ID:                  <set to the key 'gcp-project-id' in secret 'ss-secret'>                  Optional: false
      GSC_BUCKET_ID:                   <set to the key 'gsc-bucket-id' in secret 'ss-secret'>                   Optional: false
    Mounts:
      /opt/ss-config from ss-gce-access (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
Conditions:
  Type           Status
  Initialized    True 
  Ready          False 
  PodScheduled   True 
Volumes:
  ss-gce-access:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  ss-gcs-access
    Optional:    false
  default-token-4kxcq:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-4kxcq
    Optional:    false
QoS Class:       Burstable
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age                From                                                          Message
  ----     ------                 ----               ----                                                          -------
  Normal   Scheduled              29s                default-scheduler                                             Successfully assigned backend-58cdf6cd6b-rs2rs to gke-cloud-build-screenin-default-pool-d23c46b8-2hm7
  Normal   SuccessfulMountVolume  29s                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "default-token-4kxcq"
  Normal   SuccessfulMountVolume  29s                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "ss-gce-access"
  Normal   Pulling                16s (x2 over 27s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  pulling image "gcr.io/sanctionscreen/ss-backend"
  Warning  Failed                 16s (x2 over 27s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Failed to pull image "gcr.io/sanctionscreen/ss-backend": rpc error: code = Unknown desc = Error: Status 405 trying to pull repository sanctionscreen/ss-backend: "v1 Registry API is disabled. If you are not explicitly using the v1 Registry API, it is possible your v2 image could not be found. Verify that your image is available, or retry with `dockerd --disable-legacy-registry`. See https://cloud.google.com/container-registry/docs/support/deprecation-notices"
  Warning  Failed                 16s (x2 over 27s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Error: ErrImagePull
  Normal   BackOff                15s (x5 over 24s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Back-off pulling image "gcr.io/sanctionscreen/ss-backend"
  Warning  Failed                 15s (x5 over 24s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Error: ImagePullBackOff
  Normal   SandboxChanged         14s (x7 over 26s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Pod sandbox changed, it will be killed and re-created.
Hungs-MBP:screening hungbang$ docker pull gcr.io/sanctionscreen/ss-backend
Using default tag: latest
Error response from daemon: manifest for gcr.io/sanctionscreen/ss-backend:latest not found
Hungs-MBP:screening hungbang$ docker pull gcr.io/sanctionscreen/ss-backend
Using default tag: latest
Error response from daemon: manifest for gcr.io/sanctionscreen/ss-backend:latest not found
Hungs-MBP:screening hungbang$ docker pull gcr.io/sanctionscreen/ss-backend
Using default tag: latest
Error response from daemon: manifest for gcr.io/sanctionscreen/ss-backend:latest not found
Hungs-MBP:screening hungbang$ docker pull gcr.io/sanctionscreen/ss-frontend:d2d695662f6b1df97a60de71192350de980000c1
d2d695662f6b1df97a60de71192350de980000c1: Pulling from sanctionscreen/ss-frontend
ff3a5c916c92: Already exists 
b4f3ef22ce5b: Already exists 
8a6541d11dc3: Already exists 
7e869e2dcf68: Already exists 
3637be647974: Pulling fs layer 
441ad03622b0: Pulling fs layer 
c55909b4f13d: Pulling fs layer 
d4871d05141a: Waiting 
c21b4c9d63d5: Waiting 
1d935eb39805: Waiting 
86a1dc945ff5: Waiting 
1f9ad0e208eb: Waiting 
c291575dba6c: Waiting 
a9c66b38dec7: Waiting 
94fce50fc459: Waiting 
69906fcbe48f: Waiting 
^C
Hungs-MBP:screening hungbang$ kubectl apply -f k8s-backend/backend-deployment.yaml,k8s-frontend/frontend-deployment.yaml 
deployment.extensions/backend configured
deployment.extensions/frontend configured
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS              RESTARTS   AGE
pod/backend-9bcc7c9cf-2hmfd          0/1       ContainerCreating   0          8s
pod/elasticsearch-55cd497bdf-nk7wb   1/1       Running             0          36m
pod/frontend-5746667bb6-blrgr        0/1       ContainerCreating   0          9s
pod/kibana-986f6847f-v67v9           1/1       Running             0          2h
pod/redis-9dcd8d797-7khrz            1/1       Running             0          2h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)                         AGE
service/backend         LoadBalancer   10.23.244.73    104.198.150.214   8080:31386/TCP,8000:31447/TCP   31m
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235    9300:32235/TCP,9200:30118/TCP   2h
service/frontend        LoadBalancer   10.23.244.47    35.193.50.159     4200:30752/TCP                  31m
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107    5601:31472/TCP                  2h
service/kubernetes      ClusterIP      10.23.240.1     <none>            443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48     6379:31018/TCP                  2h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/backend         1         1         1            0           18m
deployment.extensions/elasticsearch   1         1         1            1           36m
deployment.extensions/frontend        1         1         1            0           18m
deployment.extensions/kibana          1         1         1            1           2h
deployment.extensions/redis           1         1         1            1           2h
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS                       RESTARTS   AGE
pod/backend-9bcc7c9cf-2hmfd          0/1       CreateContainerConfigError   0          1m
pod/elasticsearch-55cd497bdf-nk7wb   1/1       Running                      0          37m
pod/frontend-5746667bb6-blrgr        0/1       CreateContainerConfigError   0          1m
pod/kibana-986f6847f-v67v9           1/1       Running                      0          2h
pod/redis-9dcd8d797-7khrz            1/1       Running                      0          2h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)                         AGE
service/backend         LoadBalancer   10.23.244.73    104.198.150.214   8080:31386/TCP,8000:31447/TCP   32m
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235    9300:32235/TCP,9200:30118/TCP   2h
service/frontend        LoadBalancer   10.23.244.47    35.193.50.159     4200:30752/TCP                  32m
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107    5601:31472/TCP                  2h
service/kubernetes      ClusterIP      10.23.240.1     <none>            443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48     6379:31018/TCP                  2h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/backend         1         1         1            0           19m
deployment.extensions/elasticsearch   1         1         1            1           37m
deployment.extensions/frontend        1         1         1            0           19m
deployment.extensions/kibana          1         1         1            1           2h
deployment.extensions/redis           1         1         1            1           2h
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS                       RESTARTS   AGE
pod/backend-9bcc7c9cf-2hmfd          0/1       CreateContainerConfigError   0          1m
pod/elasticsearch-55cd497bdf-nk7wb   1/1       Running                      0          37m
pod/frontend-5746667bb6-blrgr        0/1       CreateContainerConfigError   0          1m
pod/kibana-986f6847f-v67v9           1/1       Running                      0          2h
pod/redis-9dcd8d797-7khrz            1/1       Running                      0          2h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)                         AGE
service/backend         LoadBalancer   10.23.244.73    104.198.150.214   8080:31386/TCP,8000:31447/TCP   32m
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235    9300:32235/TCP,9200:30118/TCP   2h
service/frontend        LoadBalancer   10.23.244.47    35.193.50.159     4200:30752/TCP                  32m
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107    5601:31472/TCP                  2h
service/kubernetes      ClusterIP      10.23.240.1     <none>            443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48     6379:31018/TCP                  2h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/backend         1         1         1            0           19m
deployment.extensions/elasticsearch   1         1         1            1           37m
deployment.extensions/frontend        1         1         1            0           19m
deployment.extensions/kibana          1         1         1            1           2h
deployment.extensions/redis           1         1         1            1           2h
Hungs-MBP:screening hungbang$ kubectl describe pod backend-9bcc7c9cf-2hmfd
Name:           backend-9bcc7c9cf-2hmfd
Namespace:      default
Node:           gke-cloud-build-screenin-default-pool-d23c46b8-2hm7/10.128.0.3
Start Time:     Fri, 02 Nov 2018 00:25:08 +0700
Labels:         io.kompose.service=backend
                pod-template-hash=567737579
Annotations:    kubernetes.io/limit-ranger=LimitRanger plugin set: cpu request for container ss-backend
Status:         Pending
IP:             10.20.1.22
Controlled By:  ReplicaSet/backend-9bcc7c9cf
Containers:
  ss-backend:
    Container ID:   
    Image:          gcr.io/sanctionscreen/ss-backend:d2d695662f6b1df97a60de71192350de980000c1
    Image ID:       
    Ports:          8080/TCP, 8000/TCP
    Host Ports:     0/TCP, 0/TCP
    State:          Waiting
      Reason:       CreateContainerConfigError
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:  100m
    Environment:
      ES_JAVA_OPTS:                    -Xms1g -Xmx3g
      CHARGEBEE_API_KEY:               <set to the key 'chargebee-api-key' in secret 'ss-secret'>               Optional: false
      CHARGEBEE_SITE:                  <set to the key 'chargebee-site' in secret 'ss-secret'>                  Optional: false
      CHARGEBEE_DEFAULT_PLAN:          <set to the key 'chargebee-default-plan' in secret 'ss-secret'>          Optional: false
      AUTH0_DOMAIN:                    <set to the key 'auth0-domain' in secret 'ss-secret'>                    Optional: false
      AUTH0_ISSUER:                    <set to the key 'auth0-issuer' in secret 'ss-secret'>                    Optional: false
      AUTH0_CLIENT_ID:                 <set to the key 'auth0-client-id' in secret 'ss-secret'>                 Optional: false
      AUTH0_API_AUDIENCE:              <set to the key 'auth0-api-audience' in secret 'ss-secret'>              Optional: false
      AUTH0_API_TOKEN:                 <set to the key 'auth0-api-token' in secret 'ss-secret'>                 Optional: false
      GOOGLE_APPLICATION_CREDENTIALS:  <set to the key 'google-application-credentials' in secret 'ss-secret'>  Optional: false
      GCP_PROJECT_ID:                  <set to the key 'gcp-project-id' in secret 'ss-secret'>                  Optional: false
      GSC_BUCKET_ID:                   <set to the key 'gsc-bucket-id' in secret 'ss-secret'>                   Optional: false
    Mounts:
      /opt/ss-config from ss-gce-access (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
Conditions:
  Type           Status
  Initialized    True 
  Ready          False 
  PodScheduled   True 
Volumes:
  ss-gce-access:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  ss-gcs-access
    Optional:    false
  default-token-4kxcq:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-4kxcq
    Optional:    false
QoS Class:       Burstable
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age               From                                                          Message
  ----     ------                 ----              ----                                                          -------
  Normal   Scheduled              1m                default-scheduler                                             Successfully assigned backend-9bcc7c9cf-2hmfd to gke-cloud-build-screenin-default-pool-d23c46b8-2hm7
  Normal   SuccessfulMountVolume  1m                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "default-token-4kxcq"
  Normal   SuccessfulMountVolume  1m                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  MountVolume.SetUp succeeded for volume "ss-gce-access"
  Normal   SandboxChanged         1m                kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Pod sandbox changed, it will be killed and re-created.
  Normal   Pulled                 40s (x7 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Successfully pulled image "gcr.io/sanctionscreen/ss-backend:d2d695662f6b1df97a60de71192350de980000c1"
  Warning  Failed                 40s (x7 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  Error: secrets "ss-secret" not found
  Normal   Pulling                27s (x8 over 1m)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-2hm7  pulling image "gcr.io/sanctionscreen/ss-backend:d2d695662f6b1df97a60de71192350de980000c1"
Hungs-MBP:screening hungbang$ kubectl get secret
NAME                  TYPE                                  DATA      AGE
default-token-4kxcq   kubernetes.io/service-account-token   3         37d
ss-gcs-access         Opaque                                1         2h
ss-secret-uat         Opaque                                12        2h
Hungs-MBP:screening hungbang$ kubectl apply -f k8s-backend/backend-deployment.yaml,k8s-frontend/frontend-deployment.yaml 
deployment.extensions/backend configured
deployment.extensions/frontend configured
Hungs-MBP:screening hungbang$ kubectl describe pod backend-9bcc7c9cf-2hmfd
Error from server (NotFound): pods "backend-9bcc7c9cf-2hmfd" not found
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS                       RESTARTS   AGE
pod/backend-859977b668-k28w4         1/1       Running                      0          9s
pod/elasticsearch-55cd497bdf-nk7wb   1/1       Running                      0          39m
pod/frontend-99987c5b6-24hfh         0/1       CreateContainerConfigError   0          11s
pod/kibana-986f6847f-v67v9           1/1       Running                      0          2h
pod/redis-9dcd8d797-7khrz            1/1       Running                      0          2h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)                         AGE
service/backend         LoadBalancer   10.23.244.73    104.198.150.214   8080:31386/TCP,8000:31447/TCP   34m
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235    9300:32235/TCP,9200:30118/TCP   2h
service/frontend        LoadBalancer   10.23.244.47    35.193.50.159     4200:30752/TCP                  34m
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107    5601:31472/TCP                  2h
service/kubernetes      ClusterIP      10.23.240.1     <none>            443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48     6379:31018/TCP                  2h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/backend         1         1         1            1           21m
deployment.extensions/elasticsearch   1         1         1            1           39m
deployment.extensions/frontend        1         1         1            0           21m
deployment.extensions/kibana          1         1         1            1           2h
deployment.extensions/redis           1         1         1            1           2h
Hungs-MBP:screening hungbang$ kubectl describe pod frontend-99987c5b6-24hfh
Name:           frontend-99987c5b6-24hfh
Namespace:      default
Node:           gke-cloud-build-screenin-default-pool-d23c46b8-xhws/10.128.0.2
Start Time:     Fri, 02 Nov 2018 00:28:48 +0700
Labels:         io.kompose.service=frontend
                pod-template-hash=555437162
Annotations:    kubernetes.io/limit-ranger=LimitRanger plugin set: cpu request for container ss-frontend
Status:         Pending
IP:             10.20.0.24
Controlled By:  ReplicaSet/frontend-99987c5b6
Containers:
  ss-frontend:
    Container ID:   
    Image:          gcr.io/sanctionscreen/ss-frontend:d2d695662f6b1df97a60de71192350de980000c1
    Image ID:       
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Waiting
      Reason:       CreateContainerConfigError
    Ready:          False
    Restart Count:  0
    Requests:
      cpu:  100m
    Environment:
      NODE_ENV:         <set to the key 'node-env' in secret 'ss-secret'>             Optional: false
      AUTH0_CLIENT_ID:  <set to the key 'auth0-client-id' in secret 'ss-secret-uat'>  Optional: false
      AUTH0_DOMAIN:     <set to the key 'auth0-domain' in secret 'ss-secret-uat'>     Optional: false
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-4kxcq (ro)
Conditions:
  Type           Status
  Initialized    True 
  Ready          False 
  PodScheduled   True 
Volumes:
  default-token-4kxcq:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-4kxcq
    Optional:    false
QoS Class:       Burstable
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type     Reason                 Age               From                                                          Message
  ----     ------                 ----              ----                                                          -------
  Normal   Scheduled              34s               default-scheduler                                             Successfully assigned frontend-99987c5b6-24hfh to gke-cloud-build-screenin-default-pool-d23c46b8-xhws
  Normal   SuccessfulMountVolume  34s               kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-xhws  MountVolume.SetUp succeeded for volume "default-token-4kxcq"
  Normal   Pulling                7s (x4 over 33s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-xhws  pulling image "gcr.io/sanctionscreen/ss-frontend:d2d695662f6b1df97a60de71192350de980000c1"
  Normal   Pulled                 7s (x4 over 33s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-xhws  Successfully pulled image "gcr.io/sanctionscreen/ss-frontend:d2d695662f6b1df97a60de71192350de980000c1"
  Warning  Failed                 7s (x4 over 33s)  kubelet, gke-cloud-build-screenin-default-pool-d23c46b8-xhws  Error: secrets "ss-secret" not found
Hungs-MBP:screening hungbang$ kubectl apply -f k8s-frontend/frontend-deployment.yaml 
deployment.extensions/frontend configured
Hungs-MBP:screening hungbang$ kubectl get pods,svc,deployment
NAME                                 READY     STATUS    RESTARTS   AGE
pod/backend-859977b668-k28w4         1/1       Running   3          2m
pod/elasticsearch-55cd497bdf-nk7wb   1/1       Running   0          41m
pod/frontend-8568c4d585-ntkbb        1/1       Running   0          54s
pod/kibana-986f6847f-v67v9           1/1       Running   0          2h
pod/redis-9dcd8d797-7khrz            1/1       Running   0          2h

NAME                    TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)                         AGE
service/backend         LoadBalancer   10.23.244.73    104.198.150.214   8080:31386/TCP,8000:31447/TCP   36m
service/elasticsearch   LoadBalancer   10.23.244.254   104.197.65.235    9300:32235/TCP,9200:30118/TCP   2h
service/frontend        LoadBalancer   10.23.244.47    35.193.50.159     4200:30752/TCP                  36m
service/kibana          LoadBalancer   10.23.241.77    35.232.212.107    5601:31472/TCP                  2h
service/kubernetes      ClusterIP      10.23.240.1     <none>            443/TCP                         37d
service/redis           LoadBalancer   10.23.240.115   35.226.200.48     6379:31018/TCP                  2h

NAME                                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/backend         1         1         1            1           23m
deployment.extensions/elasticsearch   1         1         1            1           41m
deployment.extensions/frontend        1         1         1            1           23m
deployment.extensions/kibana          1         1         1            1           2h
deployment.extensions/redis           1         1         1            1           2h
Hungs-MBP:screening hungbang$ 
>`
