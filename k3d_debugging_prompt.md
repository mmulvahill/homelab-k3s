!multi

I have a pod in my k3d cluster that is failing to start.  Help me debug the issue.  Here is the pod description

"""
> kubectl describe pod airflow-65b7c78bf8-hv9n8 -n homelab
Name:             airflow-65b7c78bf8-hv9n8
Namespace:        homelab
Priority:         0
Service Account:  default
Node:             k3d-homelab-server-0/172.19.0.3
Start Time:       Thu, 06 Feb 2025 00:38:15 -0600
Labels:           app=airflow
                  pod-template-hash=65b7c78bf8
Annotations:      <none>
Status:           Running
IP:               10.42.0.13
IPs:
  IP:           10.42.0.13
Controlled By:  ReplicaSet/airflow-65b7c78bf8
Containers:
  airflow:
    Container ID:   containerd://030b17691d9f1386fa50286fb0c92a792195866672d521ebe22de295ae67521d
    Image:          apache/airflow:latest-python3.12
    Image ID:       docker.io/apache/airflow@sha256:04e7fba174eb5c77057f59ef18c1215179181cd5dd7189afbc39b1
146f54540f
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Waiting
      Reason:       CrashLoopBackOff
    Last State:     Terminated
      Reason:       Error
      Exit Code:    2
      Started:      Thu, 06 Feb 2025 00:41:38 -0600
      Finished:     Thu, 06 Feb 2025 00:41:42 -0600
    Ready:          False
    Restart Count:  5
    Liveness:       http-get http://:8080/health delay=30s timeout=1s period=30s #success=1 #failure=3
    Readiness:      http-get http://:8080/health delay=10s timeout=1s period=10s #success=1 #failure=3
    Environment:
      AIRFLOW__CORE__EXECUTOR:              LocalExecutor
      AIRFLOW__DATABASE__SQL_ALCHEMY_CONN:  postgresql+psycopg2://user:password@postgres:5432/airflow
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-jw94v (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-jw94v:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                    From               Message
  ----     ------     ----                   ----               -------
  Normal   Scheduled  5m2s                   default-scheduler  Successfully assigned homelab/airflow-65b7
c78bf8-hv9n8 to k3d-homelab-server-0
  Normal   Pulled     4m40s                  kubelet            Successfully pulled image "apache/airflow:
latest-python3.12" in 22.404s (22.404s including waiting). Image size: 415513399 bytes.
  Normal   Pulled     4m35s                  kubelet            Successfully pulled image "apache/airflow:
latest-python3.12" in 454ms (454ms including waiting). Image size: 415513399 bytes.
  Normal   Pulled     4m18s                  kubelet            Successfully pulled image "apache/airflow:
latest-python3.12" in 446ms (446ms including waiting). Image size: 415513399 bytes.
  Normal   Created    3m50s (x4 over 4m40s)  kubelet            Created container airflow
  Normal   Started    3m50s (x4 over 4m40s)  kubelet            Started container airflow
  Normal   Pulled     3m50s                  kubelet            Successfully pulled image "apache/airflow:
latest-python3.12" in 518ms (518ms including waiting). Image size: 415513399 bytes.
  Warning  BackOff    3m19s (x7 over 4m30s)  kubelet            Back-off restarting failed container airfl
ow in pod airflow-65b7c78bf8-hv9n8_homelab(b73fea8e-6917-4166-9cc4-f03fd31fa778)
  Normal   Pulling    3m5s (x5 over 5m2s)    kubelet            Pulling image "apache/airflow:latest-pytho
n3.12"
  Normal   Pulled     3m5s                   kubelet            Successfully pulled image "apache/airflow:
latest-python3.12" in 473ms (473ms including waiting). Image size: 415513399 bytes.

"""
!end
