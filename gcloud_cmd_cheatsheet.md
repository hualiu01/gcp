# remember

## project
list all available regions and quota state in gcp:

`gcloud compute regions list`


## cloud shell

### create a persistent state in cloud shell

```
INFRACLASS_REGION=us-east1
INFRACLASS_PROJECT_ID=<To be filled in>
```

```
mkdir infraclass
touch infraclass/config

echo INFRACLASS_REGION=$INFRACLASS_REGION >> ~/infraclass/config
echo INFRACLASS_PROJECT_ID=$INFRACLASS_PROJECT_ID >> ~/infraclass/config
```
```
source infraclass/config
```
Modify the ___bash profile___ `.profile` and create persistence
```
nano .profile
```
Add the following line to the EOF
```
source infraclass/config
```

Press Ctrl+O, ENTER to save the file, and then press Ctrl+X to exit nano.

## gcs

gcloud storage cp [MY_FILE] gs://[BUCKET_NAME]