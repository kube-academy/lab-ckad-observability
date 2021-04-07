
1. Create a Pod named `myredis` with the image `bitnami/redis`. Define a liveness probe and readiness probe with an initial delay of 5 seconds and the command `redis-cli PING`.

```examiner:execute-test
name: obs-readiness-liveness-pod
title: Is Pod configured with readiness and liveness probes?
autostart: true
```

<div style="margin-top: 5em;"></div>

```section:begin
title: Solution
```

1. Create a base pod manifest:

    ```bash
    k run myredis --image=bitnami/redis --env="REDIS_PASSWORD=test" $DR > myredis.yaml
    ```

1. Visit [configuring liveness, readiness](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/) and grab a livenessProbe stanza to copy in as a starting point.

1. The `readinessProbe` stanza is identify with the exception of the base field name.

1. Your resulting pod yaml specification should resemble this:

    ```yaml
    ---
    apiVersion: v1
    kind: Pod
    metadata:
      labels:
        run: myredis
      name: myredis
    spec:
      containers:
      - name: myredis
        image: bitnami/redis
        env:
        - name: REDIS_PASSWORD
          value: test
        livenessProbe:
          exec:
            command:
            - redis-cli
            - PING
          initialDelaySeconds: 5
        readinessProbe:
          exec:
            command:
            - redis-cli
            - PING
          initialDelaySeconds: 5
    ```

1. Finally, apply the yaml.

    ```bash
    k apply -f myredis.yaml
    ```

```section:end
```
