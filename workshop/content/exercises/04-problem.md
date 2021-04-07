
1. Execute the following command, which will create a pod named `tatooine`.

    ```terminal:execute
    command: kubectl apply -f observability/tatooine.yaml
    ```

    The pod appears to be crashing. Fix it. The pod should be in running state. Recreate the pod if necessary.

```examiner:execute-test
name: obs-tatooine
title: Pod tatooine should be in running state
autostart: true
```

<div style="margin-top: 5em;"></div>

```section:begin
title: Solution
```

1. To analyze the problem, begin with:

    ```bash
    k describe pod tatooine
    ```

1. In the `Events` section you should see the message:

    ```bash
    Error: failed to create containerd task: OCI runtime create failed: container_linux.go:370: starting container process caused: exec: "ssssleep": executable file not found in $PATH: unknown
    ```

1. You can either edit the existing yaml file (in the `observability` folder), or grab the yaml of the applied pod:

    ```bash
    k get pod tatooine -o yaml > tatooine.yaml
    ```

1. Edit the yaml and fix the misspelling in the command name _sleep_

1. To redeploy, first delete the pod and apply from the corrected yaml file.

    ```bash
    k delete pod tatooine
    k apply -f tatooine.yaml
    ```

```section:end
```
