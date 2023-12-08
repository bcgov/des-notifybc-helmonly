# Digital Engagement Solutions NotifyBC
A fork of the [NotifyBC helm/ directory](https://github.com/bcgov/NotifyBC/tree/main/helm) used by the GDX DES team to deploy instances of NotifyBC to OpenShift.

## Creating new versions of this chart
1. Update the `version` property in `src/Chart.yaml` to the desired version number.
2. From the `src/` directory, run the command `helm package ./` to create a `.tgz` package for the new version.
3. Move the new `.tgz` file to the `docs/` directory (`mv notify-bc-[version].tgz ../docs`).
4. Update `docs/index.yaml` to list the new package (`helm repo index ../docs`).

## Deploying to OpenShift
1. In this example we will be deploying to `dev`, so a file named `values.dev.local.yaml` should exist and contain values specific to the `dev` instance.
1. Run `helm install dev -f platform-specific/openshift.yaml -f values.yaml -f values.dev.local.yaml ./`
    - If a deployment already exists, run `helm uninstall dev` to remove it, then repeat the command above.
1. To deploy to `test`, replace `dev` with `test` in the above example.

## Deploying BuildConfig and ImageStream for NotifyBC application
```bash
# Step 1 - Go to src/ directory of repo
cd des-notifybc/src
# Step 2 - Login to OpenShift oc command line
oc login --token=secret-token --server=https://myopnshift.com
# Step 3 - Choose the tools folder
oc project 12345-tools
# step 4 - Apply deployment file
oc apply -f deployments/openshift/notify-build.yaml
```

## Upgrading from v1 to v2

### MongoDB
MongoDB was upgraded from version 4.4.4 to 7.0.2.

#### Values
The following values were changed:
- `mongodb.auth.username` was deprecated, replaced by `mongodb.auth.usernames`
- `mongodb.auth.password` was deprecated, replaced by `mongodb.auth.passwords`
- `mongodb.auth.database` was deprecated, replaced by `mongodb.auth.databases`

#### Existing databases
Databases that were created on MongoDB 4.4.4 are not compatible with 7.0.2.

Refer to the MongoDB documentation for migrating a database to MongoDB 7: https://www.mongodb.com/docs/v7.0/release-notes/7.0-upgrade-standalone/

### Redis
Redis was upgraded from version 6.2.4 to 7.2.2. No breaking changes.

