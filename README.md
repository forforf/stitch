*We interupt this README to update you on changes this fork has from the original project*:  This fork updates stitch so that it can also bundle
in libraries exposed via content distribution networks (or really just any http request). To add in an cdn library as a module, update the config file passed into stich as such:

    config.urlpaths = ['http://path/to/lib/lib.js', ... ]

If you just want to add a cdn library as a dependency, just add it to the 
dependency list

    config.dependencies ['path/to/local/dep/lib.js', 'http://path/to/cdn/dep/lib.js']


Modules are cached locally to stitch, dependencies are not.

This is still highly experimental.

Now back to your originally scheduled README ....



<img src="https://github.com/downloads/sstephenson/stitch/logo.jpg"
width=432 height=329>

Develop and test your JavaScript applications as CommonJS modules in
Node.js. Then __Stitch__ them together to run in the browser.

    npm install stitch

Bundle code in lib/ and vendor/ and serve it with [Express](http://expressjs.com/):

    var stitch  = require('stitch');
    var express = require('express');

    var package = stitch.createPackage({
      paths: [__dirname + '/lib', __dirname + '/vendor']
    });

    var app = express.createServer();
    app.get('/application.js', package.createServer());
    app.listen(3000);

Or build it to a file:

    var stitch  = require('stitch');
    var fs      = require('fs');

    var package = stitch.createPackage({
      paths: [__dirname + '/lib', __dirname + '/vendor']
    });

    package.compile(function (err, source){
      fs.writeFile('package.js', source, function (err) {
        if (err) throw err;
        console.log('Compiled package.js');
      })
    })
