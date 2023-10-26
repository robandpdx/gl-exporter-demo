# gl-exporter demo

## Prerequisites
Install [rbenv](https://github.com/rbenv/rbenv).  
Install [nvm](https://github.com/nvm-sh/nvm).  
Install [gh-gitlab-stats](https://github.com/mona-actions/gh-gitlab-stats).  
Unzip gl-exporter.zip.  
Unzip ghec-importer.zip.  

Edit setenv.sh file, populating the following environment variable:
```
export GITLAB_API_ENDPOINT=
export GITLAB_USERNAME=
export GITLAB_API_PRIVATE_TOKEN=
```

In the gl-exporter directory:  
Run `rbenv install`.  
Run `script/bootstrap`.  

In the ghec-importer directory:
```
cd ghec-importer
npm set-script prepare ""
npm install
npm link
```

## Gather stats
Source `setenv.sh` file.  

```
gh gitlab-stats --token $GITLAB_API_PRIVATE_TOKEN --output-file gl-stats.csv --hostname https://gitlab-td-robandpdx.expert-services.io/
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