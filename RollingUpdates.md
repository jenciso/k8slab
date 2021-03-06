##Get into the kubernetes source dir and make the change

```
$ cd /kubernetes/docs/user-guide/

```

##Copy the existing nginx deployment file and rename and modify content
```

$ cp -v  nginx-deployment.yaml nginx-rolling-update.yaml

```

##Update the existing image and pod has been crated with this file

```
apiVersion: v1
kind: ReplicationController
metadata:
  name: nginx-rolling-update
spec:
  replicas: 5
  template:
    metadata:
      labels:
        app: nginx-rolling-update
    spec:
      containers:
      - name: nginx-rolling-update
        image: nginx:1.7.9
        ports:
        - containerPort: 325

```

## Update it 
```
$ kubectl rolling-update nginx-rolling-update --image=nginx:1.9.1
Created nginx-rolling-update-268d35d1df1850b31556cba4dba6a256                                                                                                            

```

##Get the deployment label too

```
$ kubectl get pods -l app=nginx-rolling-update -L deployment
NAME                                                          READY     STATUS    RESTARTS   AGE       DEPLOYMENT
nginx-rolling-update-268d35d1df1850b31556cba4dba6a256-hkn9w   1/1       Running   0          42m       268d35d1df1850b31556cba4dba6a256
nginx-rolling-update-268d35d1df1850b31556cba4dba6a256-s37w4   1/1       Running   0          39m       268d35d1df1850b31556cba4dba6a256
nginx-rolling-update-268d35d1df1850b31556cba4dba6a256-x6ptu   1/1       Running   0          40m       268d35d1df1850b31556cba4dba6a256
nginx-rolling-update-9izbx                                    1/1       Running   0          30m       268d35d1df1850b31556cba4dba6a256
nginx-rolling-update-c3pdo                                    1/1       Running   0          30m       268d35d1df1850b31556cba4dba6a256
nginx-rolling-update-dmlaw                                    1/1       Running   0          30m       268d35d1df1850b31556cba4dba6a256
nginx-rolling-update-dvhzm                                    1/1       Running   0          30m       268d35d1df1850b31556cba4dba6a256
nginx-rolling-update-rv0lc                                    1/1       Running   0          30m       268d35d1df1850b31556cba4dba6a256
nginx-rolling-update-yf3yh                                    1/1       Running   0          30m       268d35d1df1850b31556cba4dba6a256
nginx-rolling-update-z5x0c                                    1/1       Running   0          30m       268d35d1df1850b31556cba4dba6a256

```

##Rollback the stuff

```

$ kubectl rolling-update nginx-rolling-update --rollback

```

##Watch out all the commands in action!!

[![asciicast](https://asciinema.org/a/6p62gcyxf06jnx7lrvk7kni4y.png)](https://asciinema.org/a/6p62gcyxf06jnx7lrvk7kni4y)
