```js
'use strict';

  

const fs = require('fs');

const express = require('express');

const app = express();

const bodyParser = require('body-parser');

const _ = require('lodash');

  

const options = {};

const flag = fs.readFileSync('./flag', 'utf-8').trim();

const docHtml = fs.readFileSync('./index.html', 'utf-8');

  

app.use(bodyParser.json());

  

app.get('/', (req, res) => {

res.send(docHtml);

});

  

app.post('/echo', (req, res) => {

const out = {

userID: req.headers['x-forwarded-for'] || req.connection.remoteAddress,

time: Date.now()

};

  

_.merge(out, req.body);

  

if (options.flag) {

out.flag = flag;

} else {

out.flag = 'disabled';

}

  

res.json(out);

process.exit(0);

});

  

app.listen(8000);
```

***Solution***

1. Use Burp Suite to capture the request and modify the get method to post method, add the content type: **application/json** and the path "/echo"
2. Read the source code and understand it
3. The "lodash" version has vulnerabilities, research it.
4. The vulnerability is called "Prototype Pollution", here is the theory and some examples:
		-[Theory](https://security.snyk.io/vuln/SNYK-JS-LODASH-73638)
		-[Examples](https://github.com/Kirill89/prototype-pollution-exploits/blob/master/lodash/README.md)