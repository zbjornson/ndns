ndns -- dns client/server library for nodejs
==============================

## Synposis

An example DNS server written with node which responds 'Hello World':

var ndns = require('ndns');

ndns.createServer('udp4', function (req, res) {
    res.setHeader(req.header);
    res.header.qr = 1;
    res.header.aa = 1;
    res.header.rd = 0;
    res.header.ra = 0;
    res.header.ancount = 0;
    for (var i = 0; i < req.q.length; i++) {
	res.q.add(req.q[i]);
	res.addRR(req.q[i].name, 3600, ndns.ns_t.txt, "hello, world");
	res.header.ancount++;
    }
    res.send();
}).bind(5300);

console.log("Server running at 0.0.0.0:5300")

To run the server, put the code into a file called example.js and execute it
with the node program:

> node example.js
Server running at 0.0.0.0:5300

All of the examples in the documentation can be run similarly.

## ndns.Server