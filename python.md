<b>Pyenv for managing multiple python environments</b>

```
brew install pyenv
pyenv help
pyenv versions
pyenv install --list
pyenv install 3.9.0
```
----
if you want to use virtual environment do the following
```
python -m venv .venv
```

----
python current version can be set by following 

```
- export PYENV_VERSION=3.7.0
- pyenv global 3.9.0
- pyenv local 3.8.6
```

note that
* pyenv global 3.9.0 => sets version in ~/.pyenv/version
* pyenv local 3.8.6 => sets version in the .python-version file of local directory

-----
<b>Version resolution by pyenv</b>

1. $PYENV_VERSION
2. .python-version
3. ~/.pyenv/version


If you want to change the python command to resolve in the same order set in 3 above then put ~/.pyenv/shims in PATH

-------
How to control the python interpret in visual studio code
By adding the following lines in
* Workspage i.e .vscode/settings.json or
* Global i.e in $HOME/Library/Application Support/Code/User/Settings.json
Now version resolution will happen when we restart the vscode. Please note that you might have to explicitly set the interpreter in vscode to use the defaultInterpreterPath which is bit of a pain and i hope microsoft fixes this.
```
{
  "[python]":{
    "editor.defaultFormatter": "ms-python.black-formatter",
    "editor.formatOnSave": true,
  },
  "python.defaultInterpreterPath": "~/.pyenv/versions/3.11.1/bin/python",
  "black-formatter.args": ["--line-length=120"]
}
```

Also The above setting is making use of black fomatter for linting and formatting needs. Flake8 linter is another popular linter.

----

