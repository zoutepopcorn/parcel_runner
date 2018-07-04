# parcel_runner

Simple parcel runner test


```javascript

import express from 'express';
const app = express()
const exec = require("child_process").exec
const proxy = require('http-proxy-middleware')

const BASE = `/html/vue/`


const PARCEL = [{
  dir: "secret",
  port: 8282
}, {
  dir: "landing",
  port: 8181
}]

const runDev = (json) => {
  const CMD = `parcel`
  const CWD = `${__dirname}${BASE}${json.dir}`;
  console.log(CWD);
  exec(CMD, {
    cwd: CWD,
  }, (error, stdout, stderr) => {
    console.log(error);
    console.log(stderr)
    console.log(stdout)
  })

  app.use('/landing', proxy({
    target: 'http://localhost:1234',
    changeOrigin: true
  }))
}

runDev(PARCEL[0])



```
