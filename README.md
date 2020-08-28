# JPMorgan-Chase-Software-Engineering-Virtual-Experience
credit: https://www.insidesherpa.com/virtual-internships/R5iK7HMxJGBgaSbvk

---
## Local Setup
1. Python 2 or Python 3, My environment is: 

``` 
xiaxii@cecilias-mbp ~ % which python
/usr/bin/python
xiaxii@cecilias-mbp ~ % which python2
/usr/bin/python2
xiaxii@cecilias-mbp ~ % which python3 
/usr/local/bin/python3

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

## Task 1: Interface with a stock price data feed
Interface with a stock price data feed and set up your system for analysis of the data

1. Prerequest
Run server and client 
Server: 
```
xiaxii@cecilias-mbp JPMC-tech-task-1-py3 % python3 server3.py   
HTTP server started on port 8080
Query received @ t2019-02-10 10:07:43.237974
Query received @ t2019-02-11 18:12:31.763344
Query received @ t2019-02-13 00:41:03.061658
Query received @ t2019-02-13 19:37:03.654348
Query received @ t2019-02-14 08:26:51.287677
...
```

Client: 
```
xiaxii@cecilias-mbp JPMC-tech-task-1-py3 % python3 client3.py
Quoted ABC at (bid:118.13, ask:116.63, price:118.13)
Quoted DEF at (bid:115.14, ask:117.87, price:115.14)
Ratio 1
Quoted ABC at (bid:118.13, ask:116.63, price:118.13)
Quoted DEF at (bid:115.14, ask:117.87, price:115.14)
Ratio 1
Quoted ABC at (bid:118.13, ask:116.63, price:118.13)
Quoted DEF at (bid:115.14, ask:117.87, price:115.14)
Ratio 1
Quoted ABC at (bid:118.13, ask:116.63, price:118.13)
Quoted DEF at (bid:115.14, ask:117.51, price:115.14)
Ratio 1
Quoted ABC at (bid:118.13, ask:116.63, price:118.13)
Quoted DEF at (bid:115.14, ask:117.51, price:115.14)
Ratio 1
```

.**Troubleshooting**: 
AttributeError: module 'urllib' has no attribute 'urlopen'
**Solution**: 
import urllib.**request**
urllib.**request**.urlopen(...)

2. Objectives

There are two incorrect things…
(1) Ratio is always 1
(2) The price of each stock is always the same as its bid_price.

3. Making changes to client3.py

(1) **getDataPoint**, change price
```
	price = (bid_price + ask_price)/2.
```

 
(2) **getRatio**, change the return 
``` 
	if (price_b==0): # avoid ZeroDivisionError
		return
	return price_a/price_b
```

(3) **main**, change
```
if __name__ == "__main__":

	# Query the price once every N seconds.
	# Get a price directory where the key-value pair is stock name-price
	for _ in range(N):
		quotes = json.loads(urllib.request.urlopen(QUERY.format(random.random())).read())

		prices = {}
		""" ----------- Update to get the ratio --------------- """
		for quote in quotes:
			stock, bid_price, ask_price, price = getDataPoint(quote)
			prices[stock] = price
			print ("Quoted %s at (bid:%s, ask:%s, price:%s)" % (stock, bid_price, ask_price, price))

		print ("Ratio %s" % (getRatio(prices['ABC'],prices['DEF'])))
```

4.  Finished
Run client3.py:
```
Quoted ABC at (bid:126.12, ask:125.84, price:125.98)
Quoted DEF at (bid:124.66, ask:125.15, price:124.905)
Ratio 1.008606540971138
Quoted ABC at (bid:126.12, ask:125.84, price:125.98)
Quoted DEF at (bid:124.66, ask:125.15, price:124.905)
Ratio 1.008606540971138
Quoted ABC at (bid:126.12, ask:125.05, price:125.58500000000001)
Quoted DEF at (bid:124.66, ask:125.15, price:124.905)
Ratio 1.005444137544534
Quoted ABC at (bid:126.12, ask:125.05, price:125.58500000000001)
Quoted DEF at (bid:124.66, ask:125.15, price:124.905)
Ratio 1.005444137544534
Quoted ABC at (bid:126.12, ask:125.05, price:125.58500000000001)
Quoted DEF at (bid:124.66, ask:125.05, price:124.85499999999999)
Ratio 1.0058467822674304
```
## Bonus Task: Unit Test
1. Pattern - **Build-Act-Assert**:
- **Build**: We first build a simulated test scenario e.g. instantiating the dummy data we will pass in the methods we’ll test, importing the class
whose methods we want to test, etc.
- **Act**: We then make some operations and call the method we want to test for
- **Assert**: We check if the output of the method we’re testing matches the expectation we have (e.g. dummy / static data of the outcome)

2. Unittest
```
import unittest

class xxxTest(unittest.TestCase):

    def test1(self):
        self.assertEqual(xx, xxxxx)

    def test2(self):
        self.assertTrue(xxxxx)
        self.assertFalse(xxxxxx)

    def test3(self):
        self.assertEqual(xxx, xxxx)

if __name__ == '__main__':
    unittest.main()
```
A testcase is created by subclassing ```unittest.TestCase```. The three individual tests are defined with methods whose names start with the letters ```test```. This naming convention informs the test runner about which methods represent tests.

## Patch file
1. git
git is a way for developers to manage code in a project especially if there’s other developers collaborating in that project too.

2. git patch 
A git patch file is just a file that you can apply to a repository to get the changes / modifications / additions another developer did on his / her machine onto your local machine. 
This isn’t the only way to do that ofcourse but this is a viable method for a head/lead developer to check your code first before merging it into the repository’s main/master branch.

3. Make a git patch file
Fire up a terminal, enter the repository via the terminal you opened (via the cd <repo_name_here> aka change directory command) and do the following commands: (one line, one command)
```
git add -A
git config user.email "<your_email_address>"
git config user.name "<your_name>"
git commit -m 'Create Patch File'
git format-patch -1 HEAD
```
The final command, i.e. git format-patch -1 HEAD, should produce the .patch file you’d want to submit to complete this module. It will be located in the directory where you executed the command.

Other Assertions: 
self.assertIsNone()
self.assertGreater(a, b)  ...a>b
self.assertLess(a, b)     ...a<b
self.assertRaises(TypeError)

## Task 2: Use JPMorgan Chase frameworks and tools
### Background
Typically, traders monitor stock prices and trading strategies by having data displayed visually on their screens in chart form. Often these charts will be accompanied by alerts that notify users when certain events occur or when preset price thresholds are hit.

JPMorgan Chase created the Perspective tool over many years to allows users to present and manipulate data feeds visually in web applications.

[Perspective](https://perspective.finos.org/) provides a set of flexible data transforms, such as pivots, filters, and aggregations. It utilizes bleeding-edge browser technology such as Web Assembly and Apache Arrow and is unmatched in browser performance. It is engineered for reliability and production-vetted on the JPMorgan Chase trading floor and is now available to the development community as Open Source. Chect it out on [github](https://github.com/finos/perspective(https://github.com/finos/perspective) page of perspective.

