1. Create a Pod named `myenv` that runs the command `sh -c "printenv && sleep 1h"`. Use the image `bitnami/kubectl`.

1. Save the logs of the pod to `myenv.log` file.

1. Delete the pod.

```examiner:execute-test
name: obs-env-log
title: Captured env pod log?
autostart: true
```

<div style="margin-top: 5em;"></div>

```section:begin
title: Solution
```

1. Create the pod

    ```bash
    k run myenv --image=bitnami/kubectl --command -- sh -c "printenv && sleep 1h"
    ```

1. Save the logs of the pod to `myenv.log` file.

    ```bash
    k logs myenv > myenv.log
    ```

1. Delete the pod.

    ```bash
    k delete pod myenv
    ```

```section:end
```
