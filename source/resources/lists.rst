=====
Lists
=====

.. http:get:: /api/v1/lists

    List of existing subscriber lists.

    :>jsonarr int id: list's unique identifier
    :>jsonarr datetime create_datetime: list's creation datetime
    :>jsonarr int create_user: list's creation :ref:`user <authentication>`'s unique identifier
    :>jsonarr datetime update_datetime: list's last update datetime
    :>jsonarr int update_user: list's last update :ref:`user <authentication>`'s unique identifier
    :>jsonarr string name: list's name
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

.. http:post:: /api/v1/lists

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
    :status 400: invalid subscriber list data

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

.. http:get:: /api/v1/lists/(int:id)

    Details of the subscriber list matching the specified ``id``.

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
        Allow: GET, PUT, DELETE, HEAD, OPTIONS, PATCH
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

    :status 404: no subscriber list match the specified ``id``

.. http:put:: /api/v1/lists/(int:id)

    Alter the subscriber list matching the specified ``id``.

    :param id: list's unique identifier
    :type id: int

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

    **Request**:

    .. sourcecode:: http

        PUT /api/v1/lists/1 HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json
        Content-Type: application/json

        {
            "name": "Altered name",
            "default_from_name": "Emailicious",
            "default_from_email": "noreply@emailicious.com",
            "default_replyto_email": "info@emailicious.com",
            "default_language": "en",
            "languages": [
                "en",
            ]
        }

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: GET, PUT, DELETE, HEAD, OPTIONS, PATCH
        Content-Type: application/json

        {
            "id": 1,
            "create_datetime": "2014-01-09T13:51:11.516441Z",
            "create_user": 1,
            "update_datetime": "2015-01-09T13:51:11.516481Z",
            "update_user": 1,
            "name": "Altered name",
            "default_from_name": "Emailicious",
            "default_from_email": "noreply@emailicious.com",
            "default_replyto_email": "info@emailicious.com",
            "default_language": "en",
            "languages": [
                "en",
            ]
        }

    :status 400: invalid subscriber list data
    :status 404: no subscriber list match the specified ``id``

.. http:patch:: /api/v1/lists/(int:id)

    Partially alter the subscriber list matching the specified ``id``.

    :param id: list's unique identifier
    :type id: int

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

    **Request**:

    .. sourcecode:: http

        PATCH /api/v1/lists/1 HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json
        Content-Type: application/json

        {
            "default_from_name": "From emailicious",
        }

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: GET, PUT, DELETE, HEAD, OPTIONS, PATCH
        Content-Type: application/json

        {
            "id": 1,
            "create_datetime": "2014-01-09T13:51:11.516441Z",
            "create_user": 1,
            "update_datetime": "2015-01-09T13:51:11.516481Z",
            "update_user": 1,
            "name": "Default",
            "default_from_name": "From emailicious",
            "default_from_email": "noreply@emailicious.com",
            "default_replyto_email": "info@emailicious.com",
            "default_language": "en",
            "languages": [
                "en",
                "fr"
            ]
        }

    :status 400: invalid subscriber list data
    :status 404: no subscriber list match the specified ``id``

.. http:delete:: /api/v1/lists/(int:id)

    Delete the subscriber list matching the specified ``id``.

    :param id: list's unique identifier
    :type id: int

    .. warning::
        Deleting a subscriber list will also irreversibly delete all
        associated mailings and statistics.

    **Request**:

    .. sourcecode:: http

        DELETE /api/v1/lists/1 HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 204 NO CONTENT
        Vary: Accept
        Allow: GET, PUT, DELETE, HEAD, OPTIONS, PATCH

    :status 204: the subscriber list was deleted successfully
    :status 404: no subscriber list match the specified ``id``
