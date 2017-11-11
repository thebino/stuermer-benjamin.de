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
run 
```
jekyll build
```

copy all files from the output directory `public` into your `httpdocs` or `public_html` directory on your webserver.



## License
(The MIT License)

Copyright © 2009-2013 Brandon Mathis

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the ‘Software’), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED ‘AS IS’, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
