# Knock Python library

Knock API access for applications written in Python.

## Documentation

See the [documentation](https://docs.knock.app) for Python usage examples.

## Installation

To install from PyPi, run the following:

```bash
pip install knockapi
```

To install from source, clone the repo and run the following:

```bash
python setup.py install
```

## Configuration

To use the library you must provide a secret API key, provided in the Knock dashboard.

```python
from knockapi import Knock
client = Knock(api_key="sk_12345")
```

## Usage

### Identifying users

```python
from knockapi import Knock
client = Knock(api_key="sk_12345")

client.users.identify(id="jhammond", data={"name": "John Hammond", "email": "jhammond@ingen.net"})
```

## Retrieving users

```python
from knockapi import Knock
client = Knock(api_key="sk_12345")

client.users.get_user(id="jhammond")
```

### Sending notifies

```python
from knockapi import Knock
client = Knock(api_key="sk_12345")

client.notify(
  name="dinosaurs-loose",
  actor="dnedry",
  recipients=["jhammond", "agrant", "imalcolm", "esattler"],
  data={
    "type": "trex",
    "priority": 1
  }
)
```

### Signing JWTs

You can use the `pyjwt` package to [sign JWTs easily](https://pyjwt.readthedocs.io/en/stable/usage.html#encoding-decoding-tokens-with-rs256-rsa).
You will need to generate an environment specific signing key, which you can find in the Knock dashboard.

If you're using a signing token you will need to pass this to your client to perform authentication.
You can read more about [clientside authentication here](https://docs.knock.app/client-integration/authenticating-users).

```python
import jwt
import os

private_key = os.getenv("KNOCK_SIGNING_KEY")
encoded = jwt.encode({"sub": "jhammond"}, private_key, algorithm="RS256")
```
