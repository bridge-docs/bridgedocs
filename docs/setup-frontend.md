# API Setup - Front-End

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
7. After the first push, you will need to enable the App Engine Admin API through the link provided on the failed build.
