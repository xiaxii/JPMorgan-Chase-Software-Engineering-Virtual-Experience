# JPMorgan-Chase-Software-Engineering-Virtual-Experience
credit: https://www.insidesherpa.com/virtual-internships/R5iK7HMxJGBgaSbvk

---
title: JPMorgan Chase Software Engineering Virtual Experience
tags: Project
---
# Task1: Interface with a stock price data feed

## Local Setup
1. Python 2 or Python 3, My environment is: 

``` 
xiaxii@cecilias-mbp ~ % which python
/usr/bin/python
xiaxii@cecilias-mbp ~ % which python2
/usr/bin/python2
xiaxii@cecilias-mbp ~ % which python3 
xiaxii@cecilias-mbp ~ % pip --version
pip 20.0.2 from /Library/Python/2.7/site-packages/pip-20.0.2-py2.7.egg/pip (python 2.7)
xiaxii@cecilias-mbp ~ % pip3 --version
pip 20.1.1 from /usr/local/lib/python3.8/site-packages/pip (python 3.8)
```
I am using Python3 for this project.

```
xiaxii@cecilias-mbp ~ % pip3 list
Package         Version
--------------- -------
pip             20.1.1
python-dateutil 2.8.1
setuptools      49.2.0
six             1.15.0
wheel           0.34.2
```

2. Clone repository:
```
git clone https://github.com/insidesherpa/JPMC-tech-task-1-py3.git
```

3. Run the script
```
python3 server3.py
python3 client3.py
```

## Rask 1: Interface with a stock price data feed
Interface with a stock price data feed and set up your system for analysis of the data

1. Prerequest
run server and client 
| Notice Type | Count |
|:------------- |:------------- |
|xiaxii@cecilias-mbp JPMC-tech-task-1-py3 % python3 server3.py <br>HTTP server started on port 8080 <br>Query received @ t2019-02-10 10:07:43.237974 <br>Query received @ t2019-02-11 18:12:31.763344 <br>Query received @ t2019-02-13 00:41:03.061658 <br>Query received @ t2019-02-13 19:37:03.654348 <br>Query received @ t2019-02-14 08:26:51.287677 | xiaxii@cecilias-mbp JPMC-tech-task-1-py3 % python3 client3.py <br>Quoted ABC at (bid:118.13, ask:116.63, price:118.13) <br>Quoted DEF at (bid:115.14, ask:117.87, price:115.14) <br>Ratio 1 <br>Quoted ABC at (bid:118.13, ask:116.63, price:118.13) <br>Quoted DEF at (bid:115.14, ask:117.87, price:115.14) <br>Ratio 1 <br>Quoted ABC at (bid:118.13, ask:116.63, price:118.13) <br>Quoted DEF at (bid:115.14, ask:117.87, price:115.14) <br>Ratio 1 <br>Quoted ABC at (bid:118.13, ask:116.63, price:118.13) <br>Quoted DEF at (bid:115.14, ask:117.51, price:115.14) <br>Ratio 1 <br>Quoted ABC at (bid:118.13, ask:116.63, price:118.13) <br>Quoted DEF at (bid:115.14, ask:117.51, price:115.14) <br>Ratio 1 |

**Troubleshooting**: 
AttributeError: module 'urllib' has no attribute 'urlopen'
**Solution**: 
import urllib.request
urllib.request.urlopen(...)

2. Objectives
There are two incorrect things…
(1) Ratio is always 1
(2) The price of each stock is always the same as its bid_price.

3. Making changes to client3.py
(1) **getDataPoint**
``` 

