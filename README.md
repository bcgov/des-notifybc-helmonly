# Digital Engagement Solutions NotifyBC

## Deploying to OpenShift
1. In this example we will be deploying to `dev`, so a file named `values.dev.local.yaml` should exist and contain values specific to the `dev` instance.
1. Run `helm install dev -f platform-specific/openshift.yaml -f values.yaml -f values.dev.local.yaml ./`
    - If a deployment already exists, run `helm uninstall dev` to remove it, then repeat the command above.
1. To deploy to `test`, replace `dev` with `test` in the above example.