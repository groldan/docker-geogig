I assume you have docker installed already (the build file and example below
refers to docker instead of docker for commands since that is how it is
packaged in Ubuntu 14.04). So all instructions below are based on 14.04 as the
host:

Change the username and email address in the bash command to run the container:

```bash
docker pull boundless/geogig:web_api
sudo docker run -e USER='name' -e EMAIL_ADDRESS='name@gmail.com' --name="geogig" -p 38080:8182  -d  boundless/geogig:web_api
```


If you want to build the image yourself using the Docker recipe then do the following:


```bash
sudo apt-get install apt-cacher-ng
```

Edit ``71-apt-cacher-ng`` to use your host's ip address.

```bash
git clone git@github.com:luipir/docker-geogig.git
cd docker-geogig
git checkout web_api
```




```bash
sudo ./build.sh
```


Its going to take a long time (and consume a chunk of bandwidth) for the build
because you have any docker base operating system images on your system and the
maven build grabs a lot of jars.

After it is installed, to run a container substitute your username and email address on the bash command below:

```bash
sudo docker docker run -e USER='name' -e EMAIL_ADDRESS='name@gmail.com' --name="geogig" -p 38080:8182  -d  boundless/geogig
```
Then from your local machine you should be able to clone the GeoGigRepo
repository that is created in the docker container:

```
geogig clone http://localhost:38080 gisdata-repo-clone
```


- Tim Sutton, February 2015
- Luigi Pirelli for Boundless, February 2016
