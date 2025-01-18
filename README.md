## python-porasuno
### Why does pip list generate a more comprehensive list than pip freeze? 
[Knowledge Source](https://stackoverflow.com/questions/18966564/pip-freeze-vs-pip-list)
```bash
$ pip list
feedparser (5.1.3)
pip (1.4.1)
setuptools (1.1.5)
wsgiref (0.1.2)
$ pip freeze
feedparser==5.1.3
wsgiref==0.1.2
```
Pip's documentation states:

|pip <option>|Description|
|---|---|
|freeze|Output installed packages in requirements format.|
|list|List installed packages.|

#### Usage
One may generate a requirements.txt via:

`pip freeze > requirements.txt`
A user can use this requirements.txt file to install all the dependencies. For instance:

`pip install -r requirements.txt`
The packages need to be in a specific format for pip to understand, such as:

#### requirements.txt
```
feedparser==5.1.3
wsgiref==0.1.2
django==1.4.2
...
```
That is the "requirements format".

Here, `django==1.4.2` implies install `django` version 1.4.2 (even though the latest is 1.6.x). <br>
If you do not specify ==1.4.2, the latest version available would be installed.

You can read more in "Virtualenv and pip Basics", and the official "Requirements File Format" documentation.

