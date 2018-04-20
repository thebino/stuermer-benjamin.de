# Documentation

### _config.yml
---
Hier sind alle Grundeinstellungen für die Website sowie octopress gespeichert.

[![Build Status](https://travis-ci.org/thebino/stuermer-benjamin.png?branch=jekyll)](https://travis-ci.org/thebino/stuermer-benjamin)


## Docker
To run jekyll inside docker, run:
```
docker-compose up
```

## Development
```
jekyll serve --host 172.17.2.50
```


## Deployment
To create the final output, run:
```
jekyll build
```

publish the output from `public` into `httpdocs` on the webserver
```
scp -rp public/* bino@hostservice.eu:/var/www/vhosts/stuermer-benjamin.de/httpdocs
```
