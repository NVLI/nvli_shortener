# Installation steps

### Installing Mongo-2.4.9
- sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
- echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
-  sudo apt-get update
- sudo apt-get install mongodb-10gen
- apt-get install mongodb-10gen=2.4.9
- mongo --version 

### Securing Mongo
- mongo
- use admin
- db.addUser( {
user: "root",
pwd: "<password>",
roles: [ "userAdminAnyDatabase",
"readWriteAnyDatabase",
"dbAdminAnyDatabase",]
});

### Installing node & forever
- sudo apt-get install git
- sudo apt-get install build-essential checkinstall
- sudo apt-get install libssl-dev
- curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash
- command -v nvm -- to test if nvm installed successfully
- nvm install 5.10.0
- nvm use 5.10.0
- nvm alias default node
- npm install
- npm install -g bower
- npm install -g forever

### Setting up the Application
- Clone the repo
- npm install


### Running the Application
- forever start --uid=nvli_shortener app.js

### Configuring nginx to forward requests
```
upstream nvli_shortener {
  server localhost:3000;
}

server {
  listen 80;

  server_name   stage-nvli.iitb.ac.in;
  access_log    /var/log/nginx/nvli-shortener.access.log;
  error_log     /var/log/nginx/nvli-shortener.error.log;

  location / {
    proxy_pass http://nvli_shortener;
  }
}
```

