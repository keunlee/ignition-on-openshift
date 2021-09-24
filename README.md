# Inductive Automation - Ignition on Openshift (Maker Edition)

## I. Create an Openshift Project

```bash
oc new-project demo-ignition
```

## II. Create Ignition Secrets

```bash
oc create secret generic ignition-secrets \
--from-literal=IGNITION_LICENSE_KEY=REPLACE \
--from-literal=IGNITION_ACTIVATION_TOKEN=REPLACE
```

## III. Deploy Ignition

```bash
# from the root of the source repository
oc apply -k .
```

## IV. Create a Uri Route

```bash
oc expose deployment/ignition
oc expose svc/ignition
ignition_uri=$(oc get routes ignition -o 'jsonpath={.spec.host}')

# print the full uri and navigate to that in your browser
echo http://$ignition_uri
```


