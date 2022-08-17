# Animals.town - smart contracts and website

https://animals.town

1. Edit .secret and put there a wallet mnemonic phrase (24 words) - you need to have some gas on it
2. Register on polygonscan.com, bscscan.com and create a new API keys
3. Edit .apikey_* files and add your api keys on the first line of each file (* means block explorer name, e.g.: polygonscan, bscscan ...)
4. edit ./migrations/2_deploy_contracts.js and set variables
5. edit ./web/build.sh and set a different web root where you'd like to deploy your web page
6. Install dependencies and run deploy script:
```console
yarn install
./deploy.sh
```

# Used dependencies
- Hardhat
- Solidity
- Node v16.x (do not use 17.x!)
- NPM
- Yarn

# Web page
You can also build web page manualy without deploying new smart contracts using:
```console
cd ./web
./build.sh
```

You can proxy pass test version to port 80 using Nginx:
```console
server {
    listen 80;
    listen [::]:80;
    root /data/www/test.animals.town;
    index index.html index.htm;
    server_name test.animals.town;
    access_log /data/log/nginx/test.animals.town.access.log;
    error_log /data/log/nginx/test.animals.town.error.log;

    location / {
        proxy_pass http://127.0.0.1:4001;
        #try_files $uri /index.html;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

