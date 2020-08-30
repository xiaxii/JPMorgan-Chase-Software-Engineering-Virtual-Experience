# JPMorgan-Chase-Software-Engineering-Virtual-Experience
credit: https://www.insidesherpa.com/virtual-internships/R5iK7HMxJGBgaSbvk

---



## Task 2: Use JPMorgan Chase frameworks and tools
### Background
Typically, traders monitor stock prices and trading strategies by having data displayed visually on their screens in chart form. Often these charts will be accompanied by alerts that notify users when certain events occur or when preset price thresholds are hit.

JPMorgan Chase created the Perspective tool over many years to allows users to present and manipulate data feeds visually in web applications.

[Perspective](https://perspective.finos.org/) provides a set of flexible data transforms, such as pivots, filters, and aggregations. It utilizes bleeding-edge browser technology such as Web Assembly and Apache Arrow and is unmatched in browser performance. It is engineered for reliability and production-vetted on the JPMorgan Chase trading floor and is now available to the development community as Open Source. Chect it out on [github](https://github.com/finos/perspective) page of perspective.

### Set Up
```
xiaxii@cecilias-mbp JPMC % git --version
git version 2.26.1
xiaxii@cecilias-mbp JPMC % git clone https://github.com/insidesherpa/JPMC-tech-task-2-PY3.git
Cloning into 'JPMC-tech-task-2-PY3'...
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 57 (delta 4), reused 2 (delta 0), pack-reused 48
Receiving objects: 100% (57/57), 231.98 KiB | 2.37 MiB/s, done.
Resolving deltas: 100% (21/21), done.
```

```
xiaxii@cecilias-mbp JPMC-tech-task-2-PY3 % ls
README.md		package.json		test.csv
datafeed		public			tsconfig.json
package-lock.json	src
```
Start Server:
```
xiaxii@cecilias-mbp JPMC-tech-task-2-py3 % python3 datafeed/server3.py
HTTP server started on port 8080
```


```
xiaxii@cecilias-mbp JPMC-tech-task-2-PY3 % curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
...

xiaxii@cecilias-mbp JPMC-tech-task-2-PY3 % nvm --version
0.35.3

xiaxii@cecilias-mbp JPMC-tech-task-2-PY3 % nvm install v11.0.0
Downloading and installing node v11.0.0...
Downloading https://nodejs.org/dist/v11.0.0/node-v11.0.0-darwin-x64.tar.xz...
######################################################################### 100.0%
Computing checksum with shasum -a 256
Checksums matched!
Now using node v11.0.0 (npm v6.4.1)
xiaxii@cecilias-mbp JPMC-tech-task-2-PY3 % nvm use v11.0.0
Now using node v11.0.0 (npm v6.4.1)

xiaxii@cecilias-mbp JPMC-tech-task-2-PY3 % node -v
v11.0.0
xiaxii@cecilias-mbp JPMC-tech-task-2-PY3 % npm -v
6.4.1
```

First Run
```
npm install
npm start
```
![start the client application](https://raw.githubusercontent.com/xiaxii/JPMorgan-Chase-Software-Engineering-Virtual-Experience/master/JPMC/Screen%20Shot/Screen%20Shot%202020-08-27%20at%2011.10.09%20PM.png?token=AKL6M3IJ2DNDE7SVEAD5T2K7JB3PY)

Troubleshooting:
Error: type error: Cannot find module '@jpmorganchase/perspective'. TS2307
Solution: 
go to the your project directory and just type the command:
```
npm i @finos/perspective
```
this will install the required files in your project directory
and then goto your graph.tsx file and replace
```
import { Table } from '@jpmorganchase/perspective';
```
with this below code
```
import { Table } from '@finos/perspective';
```
Ref: https://github.com/insidesherpa/JPMC-tech-task-2/issues/47

### Code Changes
1. Making changes in **App.tsx**: change the static table into a live / updating graph



