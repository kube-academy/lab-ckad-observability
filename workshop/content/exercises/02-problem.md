
1. Create a Pod named `httptest` with image [`mccutchen/go-httpbin`](https://github.com/mccutchen/go-httpbin) and a readiness probe that checks the http endpoint of the container at path `/status/200` on port `8080`.

```examiner:execute-test
name: obs-httpbin-readiness-probe
title: Is Pod ready?
autostart: true
```

<div style="margin-top: 5em;"></div>

```section:begin
title: Solution
```

1. Begin by creating the pod yaml:

    ```bash
    k run httptest --image=mccutchen/go-httpbin $DR > httpbin.yaml
    ```

1. Edit the yaml to add the [readiness http probe](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#http-probes), optionally adding an initial delay of a few seconds.

1. The final yaml should resemble the following:

    ```yaml
    ---
    apiVersion: v1
    kind: Pod
    metadata:
      labels:
        run: httptest
      name: httptest
    spec:
      containers:
      - name: httptest
        image: mccutchen/go-httpbin
        readinessProbe:
          httpGet:
            path: /status/200
            port: 8080
          initialDelaySeconds: 5
    ```

1. Apply the yaml.

    ```bash
    k apply -f httpbin.yaml
    ```

```section:end
```
