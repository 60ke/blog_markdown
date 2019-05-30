# mac下的Python2的mysql模块

```python
brew install mysql
brew unlink mysql
brew install mysql-connector-c
sed -i -e 's/libs="$libs -l "/libs="$libs -lmysqlclient -lssl -lcrypto"/g' /usr/local/bin/mysql_config
pip install MySQL-python
brew unlink mysql-connector-c
brew link --overwrite mysql
```



1. `brew unlink mysql # only if installed, causes the next step to fail`

2. `brew install mysql-connector-c`

3. locate `mysql_config` file with `which (mysql_config)`

4. edit the `mysql_config` file, under `# Create options` change this:

    `libs="$libs -l "`

    to this:

    `libs="$libs -lmysqlclient -lssl -lcrypto"`

    if using vim, `:wq!` to save the read-only file

5. Now the install should run successfully

    `pip install mysqlclient`

6. Adding this separately, as it's similar but not directly related to the initial question

    `pip install MySQL-python`

7. Fix `mysql` brew formula, if it was unlinked in the first step.

    `brew unlink mysql-connector-c`

    `brew link mysql`