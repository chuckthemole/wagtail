<<<<<<< HEAD
docker-wagtail-develop
======================


A script to painlessly set up a Docker environment for development of Wagtail - inspired by [vagrant-wagtail-develop](https://github.com/wagtail/vagrant-wagtail-develop)

Initial work in Bristol sprint January 2020 by [esperk](https://github.com/esperk) and [saevarom](https://github.com/saevarom).

Setup
-----

**Requirements:** [Docker](https://www.docker.com/) and Docker Compose (Docker Compose is included with Docker Desktop for Mac and Windows).

Open a terminal and follow those instructions:

```sh
# 1. Decide where to put the project. We use "~/Development" in our examples.
cd ~/Development
# 2. Clone the docker-wagtail-develop repository in a new "wagtail-dev" folder.
git clone git@github.com:wagtail/docker-wagtail-develop.git wagtail-dev
# 3. Move inside the new folder.
cd wagtail-dev/
# 4. Run the setup script. This will check out all the dependency repos.
./setup.sh
# 5. Build the containers
docker-compose build
```

It can take a while (typically 15-20 minutes) to fetch and build all dependencies and containers.

Here is the resulting folder structure:

```sh
.
├── libs          # Supporting libraries to develop Wagtail against.
├── wagtail       # Wagtail repository / codebase.
└── bakerydemo    # Wagtail Bakery project used for development.
```

Once setup is over,

```sh
# 6. Start your container setup
docker-compose up
# Success!
```

If you're running this on Linux you might get into some privilege issues that can be solved using this command (tested on Ubuntu):
```sh
CURRENT_UID=$(id -u):$(id -g) docker-compose -f docker-compose.yml -f docker-compose.linux.yml up
```

- Visit your site at http://localhost:8000
- The admin interface is at http://localhost:8000/admin/ - log in with `admin` / `changeme`.

What you can do
---------------

### See a list of running containers

```sh
$ docker-compose ps
              Name                             Command               State           Ports
---------------------------------------------------------------------------------------------------
docker-wagtail-develop_db_1         docker-entrypoint.sh postgres    Up      5432/tcp
docker-wagtail-develop_frontend_1   /bin/sh -c cp -r /node_mod ...   Up
docker-wagtail-develop_web_1        /bin/bash -c cd /code/wagt ...   Up      0.0.0.0:8000->8000/tcp
```

### You can open a django shell session

```sh
docker-compose exec web python manage.py shell
```

### You can open a shell on the web server

```sh
docker-compose exec web bash
```

### You can open a shell to work with the frontend code (Node/NPM)

```sh
docker-compose exec frontend bash
```

Getting ready to contribute
---------------------------

Here are other actions you will likely need to do to make your first contribution to Wagtail.

Set up git remotes to Wagtail forks (run these lines outside of the Docker instances, on your machine):

```sh
cd ~/Development/wagtail-dev/wagtail
# Change the default origin remote to point to your fork.
git remote set-url origin git@github.com:<USERNAME>/wagtail.git
# Add wagtail/wagtail as the "upstream" remote.
git remote add upstream git@github.com:wagtail/wagtail.git
# Pull latest changes from all remotes / forks.
git pull --all
```


TODO
----

* Set up an elasticsearch service container
* Test on Windows and Linux
=======
<h1 align="center">
    <img width="343" src="https://cdn.jsdelivr.net/gh/wagtail/wagtail@master/.github/wagtail.svg" alt="Wagtail">
    <br>
    <br>
</h1>

Wagtail is an open source content management system built on Django, with a strong community and commercial support. It's focused on user experience, and offers precise control for designers and developers.

![Wagtail screenshot](https://cdn.jsdelivr.net/gh/wagtail/wagtail@master/.github/wagtail-screenshot-with-browser.png)

### Features

* A fast, attractive interface for authors
* Complete control over front-end design and structure
* Scales to millions of pages and thousands of editors
* Fast out of the box, cache-friendly when you need it
* Content API for 'headless' sites with de-coupled front-end
* Runs on a Raspberry Pi or a multi-datacenter cloud platform 
* StreamField encourages flexible content without compromising structure
* Powerful, integrated search, using Elasticsearch or PostgreSQL
* Excellent support for images and embedded content
* Multi-site and multi-language ready
* Embraces and extends Django

Find out more at [wagtail.io](https://wagtail.io/).

### Getting started

Wagtail works with [Python 3](https://www.python.org/downloads/), on any platform.

To get started with Wagtail, run the following in a virtual environment:

``` bash
pip install wagtail
wagtail start mysite
cd mysite
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

For detailed installation and setup docs, see [docs.wagtail.io](https://docs.wagtail.io/).

### Who’s using it?

Wagtail is used by NASA, Google, Oxfam, the NHS, Mozilla, MIT, the Red Cross, Salesforce, NBC, BMW, and the US and UK governments. Add your own Wagtail site to [madewithwagtail.org](https://madewithwagtail.org).

### Documentation

[docs.wagtail.io](https://docs.wagtail.io/) is the full reference for Wagtail, and includes guides for developers, designers and editors, alongside release notes and our roadmap.

### Compatibility

_(If you are reading this on GitHub, the details here may not be indicative of the current released version - please see [Compatible Django / Python versions](https://docs.wagtail.io/en/stable/releases/upgrading.html#compatible-django-python-versions) in the Wagtail documentation.)_

Wagtail supports:

* Django 2.2.x and 3.0.x
* Python 3.6, 3.7 and 3.8
* PostgreSQL, MySQL and SQLite as database backends

[Previous versions of Wagtail](https://docs.wagtail.io/en/stable/releases/upgrading.html#compatible-django-python-versions) additionally supported Python 2.7 and Django 1.x.

---

### Community Support

There is an active community of Wagtail users and developers responding to questions on [Stack Overflow](https://stackoverflow.com/questions/tagged/wagtail). When posting questions, please read Stack Overflow's advice on [how to ask questions](https://stackoverflow.com/help/how-to-ask) and remember to tag your question "wagtail".

For topics and discussions that do not fit Stack Overflow's question and answer format, we have a [Slack workspace](https://github.com/wagtail/wagtail/wiki/Slack) and a [Wagtail Support mailing list](https://groups.google.com/forum/#!forum/wagtail). Please respect the time and effort of volunteers by not asking the same question in multiple places.

We maintain a curated list of third party packages, articles and other resources at [Awesome Wagtail](https://github.com/springload/awesome-wagtail).

### Commercial Support

Wagtail is sponsored by [Torchbox](https://torchbox.com/). If you need help implementing or hosting Wagtail, please contact us: hello@torchbox.com. See also [madewithwagtail.org/developers/](https://madewithwagtail.org/developers/) for expert Wagtail developers around the world.

### Security

We take the security of Wagtail, and related packages we maintain, seriously. If you have found a security issue with any of our projects please email us at [security@wagtail.io](mailto:security@wagtail.io) so we can work together to find and patch the issue. We appreciate responsible disclosure with any security related issues, so please contact us first before creating a Github issue.

If you want to send an encrypted email (optional), the public key ID for security@wagtail.io is 0x6ba1e1a86e0f8ce8, and this public key is available from most commonly-used keyservers.

### Release schedule

Feature releases of Wagtail are released every three months. Selected releases are designated as Long Term Support (LTS) releases, and will receive maintenance updates for an extended period to address any security and data-loss related issues. For dates of past and upcoming releases and support periods, see [Release Schedule](https://github.com/wagtail/wagtail/wiki/Release-schedule).

#### Nightly releases

To try out the latest features before a release, we also create builds from master every night. You can find instructions on how to install the latest nightly release at https://releases.wagtail.io/nightly/index.html

### Contributing

If you're a Python or Django developer, fork the repo and get stuck in! We have several developer focused channels on the [Slack workspace](https://github.com/wagtail/wagtail/wiki/Slack).

You might like to start by reviewing the [contributing guidelines](https://docs.wagtail.io/en/latest/contributing/index.html) and checking issues with the [good first issue](https://github.com/wagtail/wagtail/labels/good%20first%20issue) label.

We also welcome translations for Wagtail's interface. Translation work should be submitted through [Transifex](https://www.transifex.com/projects/p/wagtail/).

### License
[BSD](https://github.com/wagtail/wagtail/blob/master/LICENSE)

### Thanks

We thank the following organisations for their services used in Wagtail's development:

[![Browserstack](https://cdn.jsdelivr.net/gh/wagtail/wagtail@master/.github/browserstack-logo.svg)](https://www.browserstack.com/)<br>
[BrowserStack](https://www.browserstack.com/) provides the project with free access to their live web-based browser testing tool, and automated Selenium cloud testing.

[![squash.io](https://cdn.jsdelivr.net/gh/wagtail/wagtail@master/.github/squash-logo.svg)](https://www.squash.io/)<br>
[Squash](https://www.squash.io/) provides the project with free test environments for reviewing pull requests.


[![Build Status](https://api.travis-ci.org/wagtail/wagtail.svg?branch=master)](https://travis-ci.org/wagtail/wagtail)
[![License](https://img.shields.io/badge/license-BSD-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)
[![Version](https://img.shields.io/pypi/v/wagtail.svg)](https://pypi.python.org/pypi/wagtail/) 
[![Coverage](https://codecov.io/github/wagtail/wagtail/coverage.svg?branch=master)](https://codecov.io/github/wagtail/wagtail?branch=master)
[![Total alerts](https://img.shields.io/lgtm/alerts/g/wagtail/wagtail.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/wagtail/wagtail/alerts/)
[![Language grade: Python](https://img.shields.io/lgtm/grade/python/g/wagtail/wagtail.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/wagtail/wagtail/context:python)
[![Language grade: JavaScript](https://img.shields.io/lgtm/grade/javascript/g/wagtail/wagtail.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/wagtail/wagtail/context:javascript)
[![Slack](https://wagtail-slack.now.sh/badge.svg)](https://wagtail-slack.now.sh)
>>>>>>> b59a7379300fe74bbd5b536bdfeeb503d6857f8e
