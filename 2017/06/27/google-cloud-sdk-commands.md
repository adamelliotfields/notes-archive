# Google Cloud SDK Commands

### Init
Changes current project.

```
gcloud init
```

### Compute Engine

**SSH**
* Browser/Mobile Username: adam_elliot_fields
* Windows Username: Adam
* macOS Username: adamfields

*Stick to adam_elliot_fields to normalize across platforms*

```
instance-name === instance-1
project-name === hello-world-171821
zone-name === us-east1-b

gcloud compute ssh adam_elliot_fields@{instance-name} --zone "{zone-name}" --project "{project-name}"
```

### Cloud Source
* Creating a repository on the web console and attempting to push an existing Git repo did not work.
* Use the command line to create a repo and then clone it.
* Use automatic mirroring to mirror an existing GitHub repo.

**Create**

```
gcloud source repos create REPO_NAME
```

**Clone**

```
gcloud source repos clone REPO_NAME
```

**Push**  
Same as GitHub.

```
git push origin master
```
