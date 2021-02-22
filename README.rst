========================
emencia-cmsplugin-xinnia
========================

.. Note::
    This is a fork of
    `emencia-cmsplugin-zinnia <https://github.com/emencia/emencia-cmsplugin-zinnia>`_
    (which was a fork of original "cmsplugin-zinnia") to include fixes for last
    Django and DjangoCMS versions with django-blog-xinnia (a fork of django-blog-zinnia).

    Code is almost unchanged except for needed fixes and even package has renamed
    "zinnia" to "xinnia", its module has keeped the old name.

Cmsplugin-zinnia is a bridge between `django-blog-zinnia`_ and
`django-cms`_.

This package provides plugins, menus and apphook to integrate your Zinnia
powered Weblog into your django-cms Web site.

The code bundled in this application is a copy of the original
``zinnia.plugins`` module, made for forward compatibility with
django-blog-zinnia > 0.11.


.. contents::

.. _installation:

Installation
============

Once Zinnia and the CMS are installed, you simply have to register
``cmsplugin_zinnia``, in the ``INSTALLED_APPS`` section of your
project's settings.

.. _entry-placeholder:

Entries with plugins
====================

If you want to use the plugin system of django-cms in your entries, an
extended ``Entry`` with a ``PlaceholderField`` is provided in this package.

Just add this line in your project's settings to use it. ::

  ZINNIA_ENTRY_BASE_MODEL = 'cmsplugin_zinnia.placeholder.EntryPlaceholder'

.. note::
   You have to keep in mind that the default migrations bundled with Zinnia
   do not reflect the addition made by the ``EntryPlaceholder`` model.

   A solution to initialize correctly the database can be: ::

     $ python manage.py makemigrations
     $ python manage.py migrate

Tips for using the apphook
==========================

If you want to use the apphook to provide the blog functionnalities under a
specific URL handled by the CMS, remember this tip:

* Once the apphook is registered, you can remove the inclusion of
  ``'zinnia.urls'`` in ``urls.py`` and then restart the server to see it in
  full effect.

.. _settings:

Settings
========

CMSPLUGIN_ZINNIA_APP_URLS
-------------------------
**Default value:** ``['zinnia.urls']``

The URLsets used for by the Zinnia AppHook.

CMSPLUGIN_ZINNIA_APP_MENUS
--------------------------
**Default value:** ::

  ['cmsplugin_zinnia.menu.EntryMenu',
   'cmsplugin_zinnia.menu.CategoryMenu',
   'cmsplugin_zinnia.menu.TagMenu',
   'cmsplugin_zinnia.menu.AuthorMenu']

List of strings representing the path to the `Menu` class provided by the
Zinnia AppHook.

CMSPLUGIN_ZINNIA_HIDE_ENTRY_MENU
--------------------------------
**Default value:** ``True``

Boolean used for displaying or not the entries in the ``EntryMenu`` object.

CMSPLUGIN_ZINNIA_TEMPLATES
--------------------------
**Default value:** ``[]`` (Empty list)

List of tuple for extending the plugins rendering templates.

Example: ::

  CMSPLUGIN_ZINNIA_TEMPLATES = [
    ('entry_custom.html', 'Entry custom'),
    ('entry_custom_bis.html', 'Entry custom bis')
    ]

CMSPLUGIN_ZINNIA_BASE_TEMPLATES
-------------------------------
**Default value:** ::

  [('cmsplugin_zinnia/entry_list.html', _('Entry list (default)')),
   ('cmsplugin_zinnia/entry_detail.html', _('Entry detailed')),
   ('cmsplugin_zinnia/entry_slider.html', _('Entry slider'))]

Available base templates, these are the shipped template from this application.
Commonly you will prefer to use ``CMSPLUGIN_ZINNIA_TEMPLATES`` to add new
templates.

CMSPLUGIN_ZINNIA_DEFAULT_TEMPLATE
---------------------------------
**Default value:** ``None``

Initial value for ``template_to_render`` field. If empty or undefined, initial
value will be the first item of available template choices.

.. _changelog:

Changelog
=========

Previous release history can be find in
`original fork <https://github.com/emencia/emencia-cmsplugin-zinnia>`_.

