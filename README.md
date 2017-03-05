###How to deploy dev-targeted motofans catalog on Linux:
1. Install [Hugo](https://gohugo.io/overview/installing/).
1. Run
```
$ git clone --recursive git@github.com:Unsolemn/motofans-catalog.git
$ cd motofans-catalog
$ hugo server
```

###How to configure new Hugo instance with docker:
 most cases there is no reasons to use Hugo with docker, because Hugo installation procedure is quit simple. E.g. for Ubuntu just download hugo release from https://github.com/spf13/hugo/releases, then run:
```
$ sudo dpkg -i /path/to/hugo/deb/file
``` 
And that's all.
But if you like you can also start Hugo project with docker:

1. Create instance
1. [Install docker](https://docs.docker.com/engine/installation/)
1. Add user into the docker groups
1. Install [bash-hugo-runner](https://github.com/Unsolemn/bash-hugo-runner)
1. Create new site with bash-hugo-runner
1. Clone [hugo theme](https://github.com/Unsolemn/motofans-catalog-hugo-theme) into /path/to/site/themes
1. [Mount gcs](https://cloud.google.com/compute/docs/disks/gcs-buckets) content storage bucket
1. [Mount gcs](https://cloud.google.com/compute/docs/disks/gcs-buckets) public storage bucket
1. Run hugo-server with bash-hugo-runner


###How to mount storage bucket recursively allowing access to other (e.g. www-data):
```
$ gcsfuse --implicit-dirs -o allow_other <bucket-name> <path/to/mount/point>
```
###How to unmount storage bucket.
```
$ fusermount -u <path/to/mount/point>
```
or
```
$ umount <path/to/mount/point>
```
###How to transfer local folder to a bucket recursively with gsutil:
```
$ gsutil -m cp -r dir gs://my-bucket
```
###How to share publicy for gcs bucket recursively:
```
$ gsutil -m acl set -R -a public-read gs://bucket
``` 
###How to start hugo server rendering for develop branch:
```
$ hugo server -w --renderToDisk --destination public --disableLiveReload --enableGitInfo --noChmod
```
###How to run Sass in a docker container:
```
$ docker run -it -d  --name sass-lang -v "$PWD":/usr/src/myapp -w /usr/src/myapp ruby:2.1 gem install sass tail -f > /dev/null
```
