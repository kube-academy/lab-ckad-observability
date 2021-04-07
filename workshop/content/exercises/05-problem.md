
1. Review the pod specification file `observability/coruscant.yaml`. We tried to create a pod using it, but it didn't work. Fix the spec file and create a pod using the spec file.

```examiner:execute-test
name: obs-coruscant
title: Pod coruscant should be in running state
autostart: true
```

<div style="margin-top: 5em;"></div>

```section:begin
title: Solution
```

1. Try to apply the pod:

    ```bash
    k apply -f observability/coruscant.yaml
    ```

    This should produce the error:

    ```bash
    error when creating "observability/coruscant.yaml": pods "coruscant" is forbidden: error looking up service account non-default-sa: serviceaccount "non-default-sa" not found
    ```

1. To find out a valid service account name, run `k get sa`.

1. Edit the pod yaml, either remove the specified service account, or revise the service account name to `default`.

1. Apply the pod spec.

```section:end
```
