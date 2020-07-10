# Getting the user's github access token

Git stores the user's github personal access token in
the Windows credential store, as service `git:https://github.com`
with user name `PersonalAccessToken`.

Python can read this using the `keyring` module:

```python
import keyring

pat = keyring.get_password('git:https://github.com', 'PersonalAccessToken')
```
