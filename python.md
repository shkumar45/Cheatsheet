<b>Pyenv for managing multiple python environments</b>

```
pyenv help
Pyenv install 3.9.0
Pyenv global 3.9.0 => sets version in ~/.pyenv/version
pyenv local 3.8.6 => sets version in the .python-version file of local directory
```

<b>Version resolution by pyenv</b>

```
1. $PYENV_VERSION
3. .python-version
4. ~/.pyenv/version
```

If you want to change the python command to resolve in the same order set in 3 above then put ~/.pyenv/shims in PATH
