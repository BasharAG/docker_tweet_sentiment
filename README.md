# Twitter Sentiment Analysis using 
Twitter Sentiment Analysis using  Docker, ElasticSearch and Kabana

## Docker setup 

### Install Homebrew
```
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
```

###Install Virtualbox and Vagrant using Brew Cask.
```
brew tap phinze/homebrew-cask
brew install brew-cask
brew cask install virtualbox
brew cask install vagrant
```

Install boot2docker https://docs.docker.com/installation/mac/

```
vim ~/.bashrc
```
#### Add the following
```
export DOCKER_HOST=tcp://192.168.59.103:2376
export DOCKER_CERT_PATH=/Users/mary/.boot2docker/certs/boot2docker-vm
export DOCKER_TLS_VERIFY=1
```
#### Initialize boot2docker
```
boot2docker init
```

#### start virtualbox vm called boot2docker (linux allows to run docker)
```
boot2docker up 
```

#### Install docker compose 
```
sudo pip install -U docker-compose
```

## Running the example 

```
git clone https://github.com/SWDeGennaro/docker_tweet_sentiment.git
cd docker_tweet_sentiment
```
Add your credentials for your twitter api dev account to a file called config.py that looks like the config.sample.py
```
consumer_key = "Your_consumer_key_here"
consumer_secret = "Your_consumer_secret_here"
access_token = "Your_access_token_here"
access_token_secret = "Your_access_token_secret_here"
```

#### Start docker compose in dameon mode
```
docker-compose up -d
```

### docker commands
```
#view running containers
docker ps 

#view all containers
docker ps -a

#stop docker compose 
docker-compose stop

#remove all containers
docker rm $(docker ps -a -q)

#show images
docker images

#delete all images
docker rmi $(docker images | awk '{print $3}')
```

## Viewing the data
### ElasticSearch
```
#get all 
curl -XGET $(boot2docker ip):9200/sentiment/_search?pretty

#get positive sentiment
curl -XGET $(boot2docker ip):9200/sentiment/_search?q=sentiment=positive

#get negative sentiment
curl -XGET $(boot2docker ip):9200/sentiment/_search?q=sentiment=negative

#get neutral sentiment
curl -XGET $(boot2docker ip):9200/sentiment/_search?q=sentiment=negative
```
##### NOTE: You can also view the same example in the browser
### Kibana
TODO 
