# gl-exporter demo

## Prerequisites
Install [rbenv](https://github.com/rbenv/rbenv).  
Install [nvm](https://github.com/nvm-sh/nvm).  
Unzip gl-exporter.zip.  
Unzip ghec-importer.zip.  

In the gl-exporter directory:  
Run `rbenv install`.  
Run `script/bootstrap`.  

Edit setenv.sh file, populating the following environment variable:
```
export GITLAB_API_ENDPOINT=
export GITLAB_USERNAME=
export GITLAB_API_PRIVATE_TOKEN=
```

In the ghec-importer directory:
```
cd ghec-importer
npm set-script prepare ""
npm install
npm link
```

## Export from GitLab
Source `setenv.sh` file.  

```
./exe/gl_exporter --namespace mindfulrob --project superbigmonorepo -o migration_archive.tar.gz
```

## Import into GitHub
Source `setenv.sh` file.  

```
ghec-importer import -a $GITHUB_TOKEN -t $ORG migration_archive.tar.gz
```