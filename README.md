# modo2auth-py

> A Python package to generate authentication details to communicate with Modo servers

# Prerequesites

**Credentials** that are created and shared by Modo. These will be different for each environment (`int`, `prod`, `local` etc...).

- `api_identifier` - API key from Modo
- `api_secret` - API secret from Modo

These values will be used when instantiating the library.

`python` - [See docs](https://www.python.org/downloads/)

# Install

## Via `pip`
```
pip install modo2auth requests
```

## Via `pipenv`
```python
pipenv install modo2auth
```

# Example Usage
Here's an example using `TBD` to make requests. You can use your preferred method or library.

Note: if installed with `pipenv`, run shell commands via `pipenv shell`

## `POST` Example
```py
# 1. IMPORT
import requests
import modo2auth

# 2. INSTANTIATE
# get from Modo
creds = {
    "api_identifier": "...",
    "api_secret":  "..."
}
headers = {
    "Content-Type": "application/json"
}
api_host = "http://localhost:82"  # TODO: replace with stable testing env endpoint
api_uri = "/v3/checkout/list"
data = '{"start_date": "2020-05-22T00:00:00Z","end_date": "2020-05-26T00:00:00Z"}'

# 3. SEND REQUEST
response = requests.post(
    api_host+api_uri,
    headers=headers,
    data=data,
    auth=modo2auth.Sign(creds['api_identifier'], creds['api_secret'], api_uri))

print(response.text)

```



# API

## `Sign(api_identifier, api_secret, api_uri)`

Returns an instance of the `Sign` class. Intended for use with the [`requests`](https://requests.readthedocs.io/en/master/user/authentication/) package.

- `api_identifier` (string) - API key from Modo
- `api_secret` (string) - API secret from Modo
- `api_uri` (string) - Api Uri intending to call to (ex: `"/v3/checkout/list"`)

# Contributing
1. Fork this repo via Github
2. Create your feature branch (`git checkout -b feature/my-new-feature`)
3. Ensure unit tests are passing (none at the moment...)
4. Commit your changes (`git commit -am 'Add some feature'`)
5. Push to the branch (`git push origin feature/my-new-feature`)
6. Create new Pull Request via Github
   
## Development
In the root of the project:
```bash
# enter the virtual environment
pipenv shell

# ...develop away :)
```

## Publishing
Prerequisites:
1. User account on [https://pypi.org/](https://pypi.org/)
2. User with Access to [https://pypi.org/project/modo2auth/1.0.0/](https://pypi.org/project/modo2auth/1.0.0/)


```bash
# install these globally
pip3 install setuptools twine wheel
```

Build and release:
1. Edit version in `setup.py`
2. Build release package: `python3 setup.py sdist bdist_wheel`
3. Upload: `twine upload dist/*`
4. Tag with new version `git tag v1.1.0` (According to Semantec Versioning guidelines)
5. Push tags `git push --tags`
