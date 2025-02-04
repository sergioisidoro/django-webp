django-webp
===========

Returns a webp image instead of jpg, gif or png to browsers which have
support.

|Build Status| |Coverage Status|


Usage
-----

Load the ``webp`` module in your template and use the ``webp``
templatetag to point to the image you want to convert.

.. code:: html

    {% load webp %}

    {# Use webp as you would use static templatetag #}
    <img src="{% webp 'path/to/your/image.png' %}" alt="image" />
    <!--
    If the browser has support, generates:
    <img src="/static/WEBP_CACHE/path/to/your/image.webp" alt="image" />

    else, generates:
    <img src="/static/path/to/your/image.png" alt="image" />
    -->

Installation
------------

First of all, you must install the webp support. In ubuntu you can
install via apt-get:

.. code:: sh

    apt-get install libwebp-dev

Please, check `the official guide`_ for the other systems.

Then, install ``django-webp``.

.. code:: sh

    pip install django-webp

add it to ``INSTALLED_APPS`` configuration

.. code:: python

    INSTALLED_APPS = (
        'django.contrib.staticfiles',
        'django_webp',
        '...',
    )

add the django\_webp context processor

.. code:: python

    TEMPLATES = [
        {
            '...'
            'OPTIONS': {
                'context_processors': [
                    '...',
                    'django_webp.context_processors.webp',
                ],
            },
        },
    ]

Possible problems
-----------------

``django-webp`` uses ``Pillow`` to convert the images. If you’ve
installed the ``libwebp-dev`` after already installed ``Pillow``, it’s
necessary to uninstall and install it back because it needs to be
compiled with it.

Cleaning the cache
------------------

You can clean the cache running:

.. code:: sh

    python manage.py clean_webp_images

.. _the official guide: https://developers.google.com/speed/webp/docs/precompiled

.. |Build Status| image:: https://github.com/andrefarzat/django-webp/actions/workflows/django.yml/badge.svg?branch=master
   :target: https://github.com/andrefarzat/django-webp/actions/workflows/django.yml
.. |Coverage Status| image:: https://coveralls.io/repos/github/andrefarzat/django-webp/badge.svg?branch=master
   :target: https://coveralls.io/github/andrefarzat/django-webp?branch=master
