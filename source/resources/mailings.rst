.. _mailings:

========
Mailings
========

.. http:get:: /api/v1/mailings

    List of existing mailings.

    :query list: filter results by :ref:`list<lists>`'s unique identifier

    :>jsonarr int id: mailing's unique identifier
    :>jsonarr string name: mailing's unique name
    :>jsonarr int campaign: mailing's campaign unique identifier

    **Request**:

    .. sourcecode:: http

        GET /api/v1/mailings HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: GET, POST, HEAD, OPTIONS
        Content-Type: application/json

        {
            "count": 3,
            "next": null,
            "previous": null,
            "results": [
                {
                    "id": 1,
                    "name": "First mailing",
                    "campaign": null
                },
                {
                    "id": 2,
                    "name": "Mailing with campaign",
                    "campaign": 1
                },
                {
                    "id": 3,
                    "name": "Third mailing",
                    "campaign": null
                }
            ]
        }

.. http:post:: /api/v1/mailings

    Create a new mailing with variants and deliveries.

    :<json int list: :ref:`list<lists>`'s unique identifier
    :<json string name: mailing's unique name
    :<json int campaign: campaign's unique identifier
    :<json array segments: segment unique identifiers
    :<json array variants: variants
    :<json array variants.language: variant's :ref:`language<languages>`
    :<json string variants.from_name: variant's from name (defaults to :ref:`list<lists>` ``default_from_name``)
    :<json string variants.from_email: variant's from email (defaults to :ref:`list<lists>` ``default_from_email``)
    :<json string variants.replyto_email: variant's reply-to email (defaults to :ref:`list<lists>` ``default_replyto_email``)
    :<json string variants.subject: variant's subject
    :<json string variants.layout.text: variant's layout text
    :<json string variants.layout.zip_file: `data URI`_ encoded `Zip`_ variant's layout.
    :<json array variants.deliveries: deliveries
    :<json string variants.deliveries.scheduled_datetime: scheduled datetime of the delivery

    .. note::
        In order to allow files to be submitted through a request with an
        ``application/json`` content type files must be `data URI`_ encoded.

        The ``variants.layout.zip_file`` expects the submitted file to be a
        `Zip`_ archive containing the following files:

        1. An ``index.html`` file representing the content of your layout.
        2. Optional image files (``.jpg``, ``.png``, ``.gif``) located in a
           ``images`` directory. These images should be referenced relatively
           from the ``index.html`` file to be imported appropriately.

        Here's an example of how you can generate a valid layout payload using
        `Python`_:

        .. sourcecode:: python

            import StringIO
            import zipfile

            html = """<!DOCTYPE html>
            <html>
                <body>
                    Hello World!
                    <img src="images/planet.png" />
                </body>
            </html>"""

            buffer = StringIO.StringIO()
            with zipfile.ZipFile(buffer, mode='w') as archive:
                archive.writestr('index.html', html)
                archive.write('/path/to/planet.png', 'images/planet.png')

            # URI encode the Zip file.
            layout = 'data:application/zip;charset=utf-8;base64,%s' % (
                buffer.getvalue().encode('base64'),
            )

        .. _`Python`: https://www.python.org
        .. _`data URI`: https://en.wikipedia.org/wiki/Data_URI_scheme
        .. _`Zip`: https://en.wikipedia.org/wiki/Zip_(file_format)

    **Request**:

    .. sourcecode:: http

        POST /api/v1/mailings HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json
        Content-Type: application/json

        {
            "list": 1,
            "name": "Mailing",
            "variants": [
                {
                    "subject": "Hello World!",
                    "layout": {
                        "zip_file": "data:application/zip;charset=utf-8;base64,..."
                    },
                    "deliveries": [
                        {
                            "scheduled_datetime": "2017-05-15T19:30:33Z"
                        }
                    ]
                }
            ]
        }

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 201 Created
        Allow: GET, POST, HEAD, OPTIONS
        Content-Type: application/json
        Vary: Accept

        {
            "id": 1,
            "name": "Mailing",
            "list": 1,
            "campaign": null,
            "segments": [],
            "variants": [
                {
                    "from_name": "List default from name",
                    "from_email": "list@default.from.email",
                    "replyto_email": "",
                    "subject": "Hello World!",
                    "deliveries": [
                        {
                            "exclusions": [],
                            "limit": null,
                            "scheduled_datetime": "2017-05-15T19:30:33Z"
                        }
                    ],
                    "language": null,
                    "layout": {
                        "id": 1,
                        "source": "<!DOCTYPE html>\n<html>\n<body>...</body>\n</html>"
                    }
                }
            ]
        }
