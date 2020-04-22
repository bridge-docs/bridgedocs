# API Setup - Backend

## Cloud SQL
1. Enable Cloud SQL
2. Create a PostgresSQL Instance
3. Give the instance an id and password, remember these for later.
    + Set region to “us-west2” and zone “any”.
    + Set PostgresSQL version to 11.
    + Open additional configuration options.
    + Under machine type and storage, lower cpu cores to 1 shared vCPU. For everything else, default is fine.
4. Wait for instance to be created.
5. On the overview page, copy the “Instance connection name”
6. Paste this into the django-settings/settings.py file on line 27 ("HOST": "/cloudsql/[paste here],”.
7. Select your Cloud SQL instance, select “Databases”, and create a new database. Remember the name of the database you create.

## Cloud Build
1. Enable Cloud Build.
2. Under triggers, connect a repository. Follow the steps to connect to your Github repository.
3. Create a trigger called “Production-Push”.
4. Select the repository.
5. Enter “.\*Production” in branch.
    + DO NOT invert regex.
    + Select “Autodetected” for build configuration.
    + Hit Create.
6. Enable App Engine Admin role in Cloud Build settings.
7. You'll need to create a cloud container in order to run Cloud Build tests.
    + Follow the steps listed here: https://github.com/GoogleCloudPlatform/professional-services/tree/master/examples/python-cicd-with-cloudbuilder
8. After the first push, you will need to enable the App Engine Admin API through the link provided on the failed build.

## Cloud Datastore:
1. Enable Cloud Datastore.
2. Select Datastore mode.
3. Select “us-west2” for a location.
4. Create an entity.
5. Set Kind as “Key”.
6. Select custom name for the key identifier.
7. Set “Django” for the custom name.
8. Create a property with the name as "Database Name". Set the value of this property as the database name (not the instance name) from Cloud SQL.
9. Create a property with the name as "Database Password". Set the value of this property as the database instance password from Cloud SQL.
10. Create a property with the name as "Secret Key". Set the value of this property as a long string of random characters. Example: https://www.random.org/strings/?num=1&len=20&digits=on&upperalpha=on&loweralpha=on&unique=on&format=html&rnd=new.
11. Save.

## Storage Bucket
1. Create a storage bucket.
2. Copy the name of this bucket and paste it into the django-settings/settings.py file on lines 202-204.
    + GS_BUCKET_NAME = "[paste here]"
    + GS_STATIC_BUCKET_NAME = "[paste here]"
    + GS_MEDIA_BUCKET_NAME = "[paste here]"
2. Set uniform bucket-level access control.
3. Edit permissions.
    + Select "Add Members".
    + Enter "allUsers" for New Members and set role to Storage Object Viewer.

## IAM:
1. Select Service Accounts.
2. Select Create Service Account.
3. Enter `Storage Bucket Uploader` for the service account name.
4. Select the role of Storage Admin for this service account.
5. Select Create Key.
    + Select JSON format.
    + This file will get downloaded to your computer.
6. Copy the contents of this file into the gcp-storage-creds.json file, overwriting everything in that file.
7. Run `python3 manage.py collectstatic` from the project root directory to verify that files are uploaded to the storage bucket properly.
