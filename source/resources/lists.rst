=====
Lists
=====

.. http:get:: /api/v1/list

    List of existing subscriber lists.

    :>jsonarr int id: list's unique identifier
    :>jsonarr datetime create_datetime: list's creation datetime
    :>jsonarr int create_user: list's creation :ref:`user <authentication>`'s unique identifier
    :>jsonarr datetime update_datetime: list's last update datetime
    :>jsonarr string name: list's name
    :>jsonarr int update_user: list's last update :ref:`user <authentication>`'s unique identifier
    :>jsonarr string default_from_name: list's future mailings' default "from name"
    :>jsonarr email default_from_email: list's future mailings' default "from email"
    :>jsonarr email default_replyto_email: list's the future mailings' default "reply to email"
    :>jsonarr string default_language: list's default :ref:`language<languages>`
    :>jsonarr array languages: list's allowed :ref:`languages<languages>`

    **Request**:

    .. sourcecode:: http

        GET /api/v1/lists HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: GET, HEAD, OPTIONS
        Content-Type: application/json

        {
            "count": 1,
            "next": null,
            "previous": null,
            "results": [
                {
                    "id": 1,
                    "create_datetime": "2014-01-09T13:51:11.516441Z",
                    "create_user": 1,
                    "update_datetime": "2014-01-09T13:51:11.516481Z",
                    "update_user": 1,
                    "name": "Default",
                    "default_from_name": "Emailicious",
                    "default_from_email": "noreply@emailicious.com",
                    "default_replyto_email": "info@emailicious.com",
                    "default_language": "en",
                    "languages": [
                        "en",
                        "fr"
                    ]
                }
            ]
        }

.. http:post:: /api/v1/list

    Create a new subscriber list.

    :<json string name: list's name
    :<json string default_from_name: list's future mailings' default "from name"
    :<json email default_from_email: list's future mailings' default "from email"
    :<json email default_replyto_email: list's the future mailings' default "reply to email"
    :<json string default_language: list's default :ref:`language<languages>`
    :<json array languages: list's allowed :ref:`languages<languages>`

    :>json int id: list's unique identifier
    :>json datetime create_datetime: list's creation datetime
    :>json int create_user: list's creation :ref:`user <authentication>`'s unique identifier
    :>json datetime update_datetime: list's last update datetime
    :>json int update_user: list's last update :ref:`user <authentication>`'s unique identifier
    :>json string name: list's name
    :>json string default_from_name: list's future mailings' default "from name"
    :>json email default_from_email: list's future mailings' default "from email"
    :>json email default_replyto_email: list's the future mailings' default "reply to email"
    :>json string default_language: list's default :ref:`language<languages>`
    :>json array languages: list's allowed :ref:`languages<languages>`

    :status 201: list created
    :status 400: invalid request body

    **Request**:

    .. sourcecode:: http

        POST /api/v1/lists HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json
        Content-Type: application/json

        {
            "name": "Default",
            "default_from_name": "Emailicious",
            "default_from_email": "noreply@emailicious.com",
            "default_replyto_email": "info@emailicious.com",
            "default_language": "en",
            "languages": [
                "en",
                "fr"
            ]
        }

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 201 CREATED
        Vary: Accept
        Allow: GET, POST, HEAD, OPTIONS
        Content-Type: application/json

        {
            "id": 1,
            "create_datetime": "2013-02-26T17:10:21.150Z",
            "create_user": 1,
            "update_datetime": "2013-02-26T17:10:21.150Z",
            "update_user": 1,
            "name": "Default",
            "default_from_name": "Emailicious",
            "default_from_email": "noreply@emailicious.com",
            "default_replyto_email": "info@emailicious.com",
            "default_language": "en",
            "languages": [
                "en",
                "fr"
            ]
        }

.. http:get:: /api/v1/list/(int:id)

    Details of the list matching the specified ``id``.

    :param id: list's unique identifier
    :type id: int

    :>json int id: list's unique identifier
    :>json datetime create_datetime: list's creation datetime
    :>json int create_user: list's creation :ref:`user <authentication>`'s unique identifier
    :>json datetime update_datetime: list's last update datetime
    :>json int update_user: list's last update :ref:`user <authentication>`'s unique identifier
    :>json string name: list's name
    :>json string default_from_name: list's future mailings' default "from name"
    :>json email default_from_email: list's future mailings' default "from email"
    :>json email default_replyto_email: list's the future mailings' default "reply to email"
    :>json string default_language: list's default :ref:`language<languages>`
    :>json array languages: list's allowed :ref:`languages<languages>`

    **Request**:

    .. sourcecode:: http

        GET /api/v1/lists/1 HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: GET, POST, HEAD, OPTIONS
        Content-Type: application/json

        {
            "id": 1,
            "create_datetime": "2014-01-09T13:51:11.516441Z",
            "create_user": 1,
            "update_datetime": "2014-01-09T13:51:11.516481Z",
            "update_user": 1,
            "name": "Default",
            "default_from_name": "Emailicious",
            "default_from_email": "noreply@emailicious.com",
            "default_replyto_email": "info@emailicious.com",
            "default_language": "en",
            "languages": [
                "en",
                "fr"
            ]
        }

    :status 404: no list match the specified ``id``
