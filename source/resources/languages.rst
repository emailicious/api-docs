.. _languages:

=========
Languages
=========

.. http:get:: /api/v1/languages

    List of supported `ISO-639-1`_ language codes.

    :>jsonarr string code: `ISO-639-1`_ code of the language
    :>jsonarr string name: :ref:`localized<localization>` name of language

    .. _`ISO-639-1`: https://en.wikipedia.org/wiki/ISO_639-1

    **Request**:

    .. sourcecode:: http

        GET /api/v1/languages HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: GET, HEAD, OPTIONS
        Content-Type: application/json

        {
            "count": 96,
            "next": "/api/v1/languages?page=2",
            "previous": null,
            "results": [
                {
                    "code": "ab",
                    "name": "Abkhazian"
                },
                {
                    "code": "af",
                    "name": "Afrikaans"
                },
                {
                    "code": "an",
                    "name": "Aragonese"
                },
                {
                    "code": "ar",
                    "name": "Arabic"
                }
            ]
        }
