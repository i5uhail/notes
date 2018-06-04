# Handling pods in kubernetes.

__Pod Spec URL:__ 

https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.10/#pod-v1-core

## Deploying Pods
#### Life of a pod

- Pending : in progress
- Running
- Succeeded : successfully exited
- Failed
- Unknown

#### Probes
- livenessProbe : Containers are Alive
- readinessProbe : Ready to Serve Traffic

#### Resource Configs:
AKMS => Resource Configs Specs

```
apiVersion: v1
kind:
metadata:
spec:
```

#### Sample pod yaml file: 
```
apiVersion: v1
kind: Pod
metadata:
  name: vote
  labels:
    app: python
    role: vote
    version: v1
spec:
  containers:
  - name: app
  image: schoolofdevops/vote:v1
  ports:
    - containerPort: 80
      protocol: TCP
```

Spec Schema: https://kubernetes.io/docs/user-guide/pods/multi-container/

__To list supported version of apis__

```
kubectl api-versions
```

#### Launching and operating a Pod

[The Watch command: `watch -n 1  kubectl get pods,deploy,rs,svc`]

kubectl syntax 

```
kubectl
kubectl apply --help
kubectl apply -f FILE
```

To Launch pod using configs above,
```
kubectl apply -f vote-pod.yaml
```

To check pod yaml syntax: 

```
kubectl apply -f vote-pod.yaml --dry-run=true

Output:

pod "vote" created (dry run)
```

To view pods

```
kubectl get pods
kubectl get po -o wide   #po -> alias for pods
kubectl get pods vote
```

To get detailed info

```
kubectl describe pods vote
```

[Output:]

```
Name:           vote
Namespace:      default
Node:           kube-3/192.168.0.80
Start Time:     Tue, 07 Feb 2017 16:16:40 +0000
Labels:         app=voting
Status:         Running
IP:             10.40.0.2
Controllers:    <none>
Containers:
  vote:
    Container ID:       docker://48304b35b9457d627b341e424228a725d05c2ed97cc9970bbff32a1b365d9a5d
    Image:              schoolofdevops/vote:latest
    Image ID:           docker-pullable://schoolofdevops/vote@sha256:3d89bfc1993d4630a58b831a6d44ef73d2be76a7862153e02e7a7c0cf2936731
    Port:               80/TCP
    State:              Running
      Started:          Tue, 07 Feb 2017 16:16:52 +0000
    Ready:              True
    Restart Count:      0
    Volume Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-2n6j1 (ro)
    Environment Variables:      <none>
Conditions:
  Type          Status
  Initialized   True
  Ready         True
  PodScheduled  True
Volumes:
  default-token-2n6j1:
    Type:       Secret (a volume populated by a Secret)
    SecretName: default-token-2n6j1
QoS Class:      BestEffort
Tolerations:    <none>
Events:
  FirstSeen     LastSeen        Count   From                    SubObjectPath           Type            Reason          Message
  ---------     --------        -----   ----                    -------------           --------        ------          -------
  21s           21s             1       {default-scheduler }                            Normal          Scheduled       Successfully assigned vote to kube-3
  20s           20s             1       {kubelet kube-3}        spec.containers{vote}   Normal          Pulling         pulling image "schoolofdevops/vote:latest"
  10s           10s             1       {kubelet kube-3}        spec.containers{vote}   Normal          Pulled          Successfully pulled image "schoolofdevops/vote:latest"
  9s            9s              1       {kubelet kube-3}        spec.containers{vote}   Normal          Created         Created container with docker id 48304b35b945; Security:[seccomp=unconfined]
  9s            9s              1       {kubelet kube-3}        spec.containers{vote}   Normal          Started         Started container with docker id 48304b35b945

```
Commands to operate the pod

```
kubectl logs vote

kubectl exec -it vote  sh
```

__Inside the container in a pod__


```
ifconfig
cat /etc/issue
hostname
cat /proc/cpuinfo
ps aux
```

Port Forwarding

```
kubectl port-forward --help
kubectl port-forward vote 8000:80
```

### Troubleshooting Tip

If you would like to know whats the current status of the pod, and if its in a error state, find out the cause of the error, following command could be very handy.

```
kubectl get pod vote -o yaml
```

Update pod spec and change the image to something that does not exist.

```
kubectl edit pod vote
```

Editing the container image name and checking the status returns: 

```
kubectl get pods  

NAME      READY     STATUS             RESTARTS   AGE
vote      0/1       ImagePullBackOff   0          7m
```
Again running this would return more detail:

`kubectl get pod vote -o yaml`

```
    restartCount: 0
    state:
      waiting:
        message: 'rpc error: code = Unknown desc = Error response from daemon: manifest
          for schoolofdevops/vote:vasada not found'
        reason: ErrImagePull
```

## Attaching a volume to a Pod (persisting data)

Volumes are always mounted to a container and not a pod. 

Volumes are defined a different spec on the yaml file. 


create a pod for database and attach a volume to it. To achieve this we will need to

- create a volumes definition
- attach volume to container using VolumeMounts property

Local host volumes are of two types:
* emptyDir
* hostPath

We will pick hostPath. Refer to this doc to read more about hostPath. https://kubernetes.io/docs/concepts/storage/volumes/#hostpath

example pod file: 
```
apiVersion: v1
kind: Pod
metadata:
  name: db
  labels:
    app: postgres
    role: database
    tier: back
spec:
  containers:
    - name: db
      image: postgres:9.4
      ports:
        - containerPort: 5432
      volumeMounts:
        - name: pg-data
          mountPath: /var/lib/postgresql/data

  volumes:
    - name: pg-data
      hostPath:
        path: /var/lib/postgres
        type: DirectoryOrCreate
```

To create this pod,

```
kubectl apply -f db-pod.yaml
kubectl describe pod db
kubectl get events
```
#### Creating Multi Container Pods

```
apiVersion: v1
kind: Pod
metadata:
  name: web
  labels:
    tier: front
    app: nginx
    role: ui
spec:
  containers:
    - name: nginx
      image: nginx:stable-alpine
      ports:
        - containerPort: 80
          protocol: TCP
      volumeMounts:
        - name: data
          mountPath: /var/www/html-sample-app

    - name: sync
      image: schoolofdevops/sync:v2
      volumeMounts:
        - name: data
          mountPath: /var/www/app

  volumes:
    - name: data
      emptyDir: {}
```

To create this pod

```
kubectl apply -f multi_container_pod.yml
```

Check Status

```
root@kube-01:~# kubectl get pods
NAME      READY     STATUS              RESTARTS   AGE
nginx     0/2       ContainerCreating   0          7s
vote      1/1       Running             0          3m
```

Checking logs, logging in
```
kubectl logs  web  -c sync
kubectl logs  web  -c nginx

kubectl exec -it web  sh  -c nginx
kubectl exec -it web  sh  -c sync
```