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

## V. Setup

There will be an initial setup screen. 
- Select "MySql" as the database 
- Adjust the database uri/host to: "mysql-gogs:3306"
- Adjust the database password to: "password"
- Adjust the application url to: the network route defined in the previous step, http://$gogs_uri
- Leave everything else as is, scroll to the bottom and continue

![Screenshot from 2021-07-01 10-01-51](https://user-images.githubusercontent.com/61749/124146545-7aa97a00-da53-11eb-861c-36102eb02a7c.png)

You should end up at a page that looks like this:

![Screenshot from 2021-06-11 01-10-18](https://user-images.githubusercontent.com/61749/121639258-e2bb0080-ca51-11eb-89e0-c5006745efc3.png)


