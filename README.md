# python-muckrock

A simple python wrapper for the [MuckRock API](https://www.muckrock.com/api/)

Still very much experimental and incomplete.


### Getting started

Installation is as easy as:

```bash
$ pip install python-muckrock
```


### Usage

Import the MuckRock client and initialize it.

```python
>>> from muckrock import MuckRock
>>> client = MuckRock()
```

Request all of the latest FOIA requests.

```python
>>> request_list = client.foia.latest()
```

Request the latest completed FOIA requests.

```python
>>> request_list = client.foia.filter(status="done")
```

Request a particular FOIA request by its identifier.

```python
>>> request = client.foia.get(100)
```

JSON is returned.


### Authentication

To authenticate with the MuckRock API, simply supply your username and password when you instantiate the MuckRock client. This will you allow you to do things like access your embargoed requests.

```python
>>> client = MuckRock(username="my_username", password="my_password")
```

When you authenticate with the MuckRock API, it supplies a token you can re-use. You can access that token by inspecting the `token` property of your client.

```python
>>> client.token
'aaabbbcccdddeee111222333444555666777888fff'
```

Rather than putting your user name and password in your code, consider storing the token in something like an environmental variable, and using that to authenticate with the API.

```python
>>> import os
>>> from muckrock import MuckRock
>>> client = MuckRock(token=os.environ['MUCKROCK_TOKEN'])
```

### Creating requests

Once you've authenticated, you can create an information request by passing in a title, agency id and document request to the `create` method.

```python
client.foia.create(
    agency_ids=248,
    title='API Test File Request',
    document_request="I would like the government's secret receipe for the world's best burrito."
)
```
