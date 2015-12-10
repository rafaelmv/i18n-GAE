# Internationalization using i18n

We are using WebApp2 framework and Jinja2 templating system

## First we need to install *Babel* 

```shell
$ sudo pip install babel

#Download babel 1.3
$ wget https://github.com/mitsuhiko/babel/archive/1.3.zip

# unzip and enter babel source directory
$ unzip 1.3.zip
$ cd babel-1.3/

# create babel.zip for zipimport
$ zip -r babel.zip babel/*

# move babel.zip to your project root directory
```

## Install *pytz* (use *gae-pytz* for this)

```shell
# download gaepytz 2011h
$ wget https://pypi.python.org/packages/source/g/gaepytz/gaepytz-2011h.tar.gz#md5=b7abe173cd98b417fab3e91c1498cdd2

# unzip and enter gaepytz source directory
$ tar xvzf gaepytz-2011h.tar.gz
$ cd gaepytz-2011h/

# create pytz.zip for zipimport
$ zip -r pytz.zip pytz/*

# move pytz.zip to your project root directory
```

our `main.py` file is importing ours `babel.zip` and `pytz.zip` libraries 

In our `index.html` wrap the string you want to tranlsate in `{{ _("string") }}` format

## babel.cfg

The `*babel.cfg*` file tells babel to extract all translations from all HTML files in your webapp and the encoding of HTML files are utf-8

```
[javascript: **.html]
encoding = utf-8
```

## Extract and compile translations

By default, webapp2 looks for `.pot` and `.po` files in *locale* directory under your project root directory, so first create a directory named *locale*

```shell
$ mkdir locale
```

Then extract all translations (create a `.pot` file)

```shell
$ pybabel extract -F ./babel.cfg -o ./locale/messages.pot ./
```
Then initialize the directory for each locale that your webapp will support. `en_US` and `es_MX` are supported in this example


```shell
$ pybabel init -l en_US -d ./locale -i ./locale/messages.pot
$ pybabel init -l zh_TW -d ./locale -i ./locale/messages.pot
```

Two po files (`locale/en_US/LC_MESSAGES/messages.po` and `locale/es_MX/LC_MESSAGES/messages.po`) are created. 
In this files we translate our page in the `msgstr` string.

After translate we just compile the `.po` files

```shell
$ pybabel compile -f -d ./locale
```

Now we only run our server `dev_appserver.py .`

[http://localhost:8080/!](http://127.0.0.1:8080/)

And we see the translation here

[http://localhost:8080/!](http://127.0.0.1:8080/?locale=es_MX)


When we want to update the translations we re-create the `pot`, update our locales and compile the `po` files








