.. _localization:

============
Localization
============

Certain resources content is localized using `content negotiation`_ based on
the :http:header:`Accept-Language` header.

For example, the :http:get:`/api/v1/regions` resource will return localized
``name`` if a language is specified through the aforementioned header.

.. note::
    If the :http:header:`Accept-Language` header is not provided the current
    locale will be determined from the
    :ref:`authenticated user <authentication>` language if defined.

.. _`content negotiation`: https://en.wikipedia.org/wiki/Content_negotiation
