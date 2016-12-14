===========
Subscribers
===========

.. http:get:: /api/v1/lists/(int:list_id)/subscribers

    Subscribers of the list matching the specified ``list_id``.

    :param list_id: list's unique identifier
    :type list_id: int

    :query subscription: filter results by ``subscription`` status, valid values are ``active``, ``pending``, ``bounced``, ``unsubscribed`` and ``deleted``
    :query email: filter results by ``email``

    :>jsonarr int id: subscriber's unique identifier
    :>jsonarr datetime create_datetime: subscriber's creation datetime
    :>jsonarr int create_user: subscriber's creation :ref:`user <authentication>`'s unique identifier
    :>jsonarr datetime update_datetime: subscriber's last update datetime
    :>jsonarr int update_user: subscriber's last update :ref:`user <authentication>`'s unique identifier
    :>jsonarr string subscription: subscriber's subscription status
    :>jsonarr email email: subscriber's email
    :>jsonarr string first_name: subscriber's first name
    :>jsonarr string last_name: subscriber's last name
    :>jsonarr string gender: subscriber's gender
    :>jsonarr date date_of_birth: subscriber's date of birth
    :>jsonarr string language: subscriber's :ref:`language<languages>`
    :>jsonarr string region: subscriber's :ref:`region<regions>`

    .. note::
        Custom shared and list fields should also be part of the subscriber
        objects. The exact structure of the list can be retrieved by
        :ref:`introspecting<custom-fields-instropection>` the resource.

    **Request**:

    .. sourcecode:: http

        GET /api/v1/lists/1/subscribers HTTP/1.1
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
                    "create_datetime": "2014-01-09T13:51:50.549536Z",
                    "create_user": 1,
                    "update_datetime": "2015-10-08T12:32:59.330455Z",
                    "update_user": 1,
                    "subscription": "active",
                    "email": "active@example.com",
                    "first_name": "Sergio",
                    "last_name": "Leone",
                    "gender": "m",
                    "date_of_birth": "1929-01-03",
                    "language": "it",
                    "region": "IT-RM"
                },
                {
                    "id": 2,
                    "create_datetime": "2014-01-09T13:51:50.549536Z",
                    "create_user": 1,
                    "update_datetime": "2015-10-08T12:32:59.330455Z",
                    "update_user": 1,
                    "subscription": "bounced",
                    "email": "bounced@example.com",
                    "first_name": "Ennio",
                    "last_name": "Morricone",
                    "gender": "m",
                    "date_of_birth": "1928-11-10",
                    "language": "it",
                    "region": "IT-RM"
                },
                {
                    "id": 3,
                    "create_datetime": "2014-01-09T13:51:50.549536Z",
                    "create_user": 1,
                    "update_datetime": "2015-10-08T12:32:59.330455Z",
                    "update_user": 1,
                    "subscription": "deleted",
                    "email": "deleted@example.com",
                    "first_name": "Clint",
                    "last_name": "Eastwood",
                    "gender": "m",
                    "date_of_birth": "1930-05-31",
                    "language": "en",
                    "region": "US-CA"
                }
            ]
        }

    :status 404: no subscriber list match the specified ``list_id``

.. http:post:: /api/v1/lists/(int:list_id)/subscribers

    Create subscriber for the list matching the specified ``list_id``.

    :param list_id: list's unique identifier
    :type list_id: int

    :<json email email: subscriber's email
    :<json string first_name: subscriber's first name
    :<json string last_name: subscriber's last name
    :<json string gender: subscriber's gender
    :<json date date_of_birth: subscriber's date of birth
    :<json string language: subscriber's :ref:`language<languages>`
    :<json string region: subscriber's :ref:`region<regions>`

    .. note::
        Custom shared and list fields can also be specified as parameters.
        The exact structure of the list can be retrieved by
        :ref:`introspecting<custom-fields-instropection>` the resource.

    :>json int id: subscriber's unique identifier
    :>json datetime create_datetime: subscriber's creation datetime
    :>json int create_user: subscriber's creation :ref:`user <authentication>`'s unique identifier
    :>json datetime update_datetime: subscriber's last update datetime
    :>json int update_user: subscriber's last update :ref:`user <authentication>`'s unique identifier
    :>json string subscription: subscriber's subscription status
    :>json email email: subscriber's email
    :>json string first_name: subscriber's first name
    :>json string last_name: subscriber's last name
    :>json string gender: subscriber's gender
    :>json date date_of_birth: subscriber's date of birth
    :>json string language: subscriber's :ref:`language<languages>`
    :>json string region: subscriber's :ref:`region<regions>`

    **Request**:

    .. sourcecode:: http

        POST /api/v1/lists/1/subscribers HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json
        Content-Type: application/json

        {
            "email": "test@example.com",
            "first_name": "Dolly",
            "last_name": "Parton",
            "gender": "f",
            "date_of_birth": "1946-01-19",
            "language": "en",
            "region": "US-TN"
        }

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 201 CREATED
        Vary: Accept
        Allow: GET, POST, HEAD, OPTIONS
        Content-Type: application/json

        {
            "id": 1,
            "create_datetime": "2015-11-27T22:14:36.590658Z",
            "create_user": 1,
            "update_datetime": "2015-11-27T22:14:36.590711Z",
            "update_user": 1,
            "subscription": "active",
            "email": "test@example.com",
            "first_name": "Dolly",
            "last_name": "Parton",
            "gender": "f",
            "date_of_birth": "1946-01-19",
            "language": "en",
            "region": "US-TN"
        }

    :status 201: the subscriber was created successfully
    :status 400: invalid subscriber data
    :status 404: no subscriber list match the specified ``list_id``
    :status 409: a subscriber with the specified ``email`` :ref:`already exists in this list<email-conflict>`.

    .. _`email-conflict`:

    .. admonition:: Dealing with :http:statuscode:`409`

        When a list already contains a subscriber with the specified ``email``
        the conflicting subscriber will be returned in the body of a
        :http:statuscode:`409` response.

        .. sourcecode:: http

            HTTP/1.1 409 CONFLICT
            Vary: Accept
            Allow: GET, POST, HEAD, OPTIONS
            Content-Type: application/json

            {
                "id": 2,
                "create_datetime": "2015-11-27T22:14:36.590658Z",
                "create_user": 1,
                "update_datetime": "2015-11-27T22:14:36.590711Z",
                "update_user": 1,
                "subscription": "active",
                "email": "conflict@example.com",
                "first_name": "Dolly",
                "last_name": "Parton",
                "gender": "f",
                "date_of_birth": "1946-01-19",
                "language": "en",
                "region": "US-TN"
            }

        At this point your application should either notify the user behind
        the request that this ``email`` is already subscribed or proceed to
        :ref:`update the conflicting subscriber<subscriber-update>` given you
        authenticated the user as the owner of the specified ``email``
        address.

        Note that that a conflict may occur even if the subscriber previously
        unsubscribed or was deleted from the specified list. You might want to
        take different action based on the returned ``subscription`` status
        and your application's business logic such as :ref:`confirming the
        re-activation<subscription-activation>`.

.. http:options:: /api/v1/lists/(int:list_id)/subscribers

    Introspection details of the subscribers resource.

    :param list_id: list's unique identifier
    :type list_id: int

    **Request**:

    .. sourcecode:: http

        OPTIONS /api/v1/lists/1/subscribers HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: GET, POST, HEAD, OPTIONS
        Content-Type: application/json

        {
            "name": "Subscriber List",
            "renders": [
                "application/json",
                "text/html"
            ],
            "parses": [
                "application/json",
                "application/x-www-form-urlencoded",
                "multipart/form-data"
            ],
            "actions": {
                "POST": {
                    "id": {
                        "type": "integer",
                        "required": false,
                        "read_only": true,
                        "label": "ID"
                    },
                    "create_datetime": {
                        "type": "datetime",
                        "required": false,
                        "read_only": true,
                        "label": "Create datetime"
                    },
                    "create_user": {
                        "type": "field",
                        "required": false,
                        "read_only": true,
                        "label": "Create user"
                    },
                    "update_datetime": {
                        "type": "datetime",
                        "required": false,
                        "read_only": true,
                        "label": "Update datetime"
                    },
                    "update_user": {
                        "type": "field",
                        "required": false,
                        "read_only": true,
                        "label": "Update user"
                    },
                    "subscription": {
                        "type": "field",
                        "required": false,
                        "read_only": true,
                        "label": "Subscription"
                    },
                    "email": {
                        "type": "email",
                        "required": true,
                        "read_only": false,
                        "label": "Email",
                        "max_length": 254
                    },
                    "first_name": {
                        "type": "string",
                        "required": false,
                        "read_only": false,
                        "label": "First name",
                        "max_length": 100
                    },
                    "last_name": {
                        "type": "string",
                        "required": false,
                        "read_only": false,
                        "label": "Last name",
                        "max_length": 100
                    },
                    "gender": {
                        "type": "choice",
                        "required": false,
                        "read_only": false,
                        "label": "Gender",
                        "choices": [
                            {
                                "display_name": "Unknown",
                                "value": ""
                            },
                            {
                                "display_name": "Male",
                                "value": "m"
                            },
                            {
                                "display_name": "Female",
                                "value": "f"
                            }
                        ]
                    },
                    "date_of_birth": {
                        "type": "date",
                        "required": false,
                        "read_only": false,
                        "label": "Date of birth"
                    },
                    "language": {
                        "type": "field",
                        "required": false,
                        "read_only": false,
                        "label": "Language",
                        "help_text": "ISO-639-1 language code."
                    },
                    "region": {
                        "type": "field",
                        "required": false,
                        "read_only": false,
                        "label": "Region",
                        "help_text": "ISO-3166-1 country or ISO-3166-2 region code."
                    }
                }
            }
        }

    .. _`custom-fields-instropection`:

    .. admonition:: Custom fields introspection

        You can use the ``actions.POST`` details to retrieve the name and type
        of custom fields from the specified ``list_id`` structure.

    :status 404: no subscriber list match the specified ``list_id``

.. http:get:: /api/v1/lists/(int:list_id)/subscribers/(int:id)

    Details of the subscriber matching the specified ``list_id`` and ``id``.

    :param list_id: list's unique identifier
    :type list_id: int
    :param id: subscriber's unique identifier
    :type id: int

    :>json int id: subscriber's unique identifier
    :>json datetime create_datetime: subscriber's creation datetime
    :>json int create_user: subscriber's creation :ref:`user <authentication>`'s unique identifier
    :>json datetime update_datetime: subscriber's last update datetime
    :>json int update_user: subscriber's last update :ref:`user <authentication>`'s unique identifier
    :>json string subscription: subscriber's subscription status
    :>json email email: subscriber's email
    :>json string first_name: subscriber's first name
    :>json string last_name: subscriber's last name
    :>json string gender: subscriber's gender
    :>json date date_of_birth: subscriber's date of birth
    :>json string language: subscriber's :ref:`language<languages>`
    :>json string region: subscriber's :ref:`region<regions>`

    .. note::
        Custom shared and list fields should also be part of the subscriber
        object. The exact structure of the list can be retrieved by
        :ref:`introspecting<custom-fields-instropection>` the resource.

    **Request**:

    .. sourcecode:: http

        GET /api/v1/lists/1/subscribers/1 HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: GET, PUT, PATCH, DELETE, HEAD, OPTIONS
        Content-Type: application/json

        {
            "id": 1,
            "create_datetime": "2015-11-27T22:14:36.590658Z",
            "create_user": 1,
            "update_datetime": "2015-11-28T22:14:36.590711Z",
            "update_user": 1,
            "subscription": "active",
            "email": "test@example.com",
            "first_name": "Dolly",
            "last_name": "Parton",
            "gender": "f",
            "date_of_birth": "1946-01-19",
            "language": "en",
            "region": "US-TN"
        }

    :status 404: no subscriber match the specified ``list_id`` and ``id``

.. _`subscriber-update`:

.. http:put:: /api/v1/lists/(int:list_id)/subscribers/(int:id)

    Alter the subscriber matching the specified ``id`` and ``list_id``.

    :param list_id: list's unique identifier
    :type list_id: int
    :param id: subscriber's unique identifier
    :type id: int

    :<json email email: subscriber's email
    :<json string first_name: subscriber's first name
    :<json string last_name: subscriber's last name
    :<json string gender: subscriber's gender
    :<json date date_of_birth: subscriber's date of birth
    :<json string language: subscriber's :ref:`language<languages>`
    :<json string region: subscriber's :ref:`region<regions>`

    .. note::
        Custom shared and list fields can also be specified as parameters.
        The exact structure of the list can be retrieved by
        :ref:`introspecting<custom-fields-instropection>` the resource.

    :>json int id: subscriber's unique identifier
    :>json datetime create_datetime: subscriber's creation datetime
    :>json int create_user: subscriber's creation :ref:`user <authentication>`'s unique identifier
    :>json datetime update_datetime: subscriber's last update datetime
    :>json int update_user: subscriber's last update :ref:`user <authentication>`'s unique identifier
    :>json string subscription: subscriber's subscription status
    :>json email email: subscriber's email
    :>json string first_name: subscriber's first name
    :>json string last_name: subscriber's last name
    :>json string gender: subscriber's gender
    :>json date date_of_birth: subscriber's date of birth
    :>json string language: subscriber's :ref:`language<languages>`
    :>json string region: subscriber's :ref:`region<regions>`

    **Request**:

    .. sourcecode:: http

        POST /api/v1/lists/1/subscribers/1 HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json
        Content-Type: application/json

        {
            "email": "test@example.com",
            "first_name": "Altered Dolly",
            "last_name": "Parton",
            "gender": "f",
            "date_of_birth": "1946-01-19",
            "language": "en",
            "region": "US-TN"
        }

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: GET, PUT, PATCH, DELETE, HEAD, OPTIONS
        Content-Type: application/json

        {
            "id": 1,
            "create_datetime": "2015-11-27T22:14:36.590658Z",
            "create_user": 1,
            "update_datetime": "2015-11-28T22:14:36.590711Z",
            "update_user": 1,
            "subscription": "active",
            "email": "test@example.com",
            "first_name": "Altered Dolly",
            "last_name": "Parton",
            "gender": "f",
            "date_of_birth": "1946-01-19",
            "language": "en",
            "region": "US-TN"
        }

    :status 400: invalid subscriber data
    :status 404: no subscriber match the specified ``list_id`` and ``id``
    :status 409: a subscriber with the specified ``email`` :ref:`already exists in this list<email-conflict>`.

.. http:patch:: /api/v1/lists/(int:list_id)/subscribers/(int:id)

    Partially alter the subscriber matching the specified ``id`` and ``list_id``.

    :param list_id: list's unique identifier
    :type list_id: int
    :param id: subscriber's unique identifier
    :type id: int

    :<json email email: subscriber's email
    :<json string first_name: subscriber's first name
    :<json string last_name: subscriber's last name
    :<json string gender: subscriber's gender
    :<json date date_of_birth: subscriber's date of birth
    :<json string language: subscriber's :ref:`language<languages>`
    :<json string region: subscriber's :ref:`region<regions>`

    .. note::
        Custom shared and list fields can also be specified as parameters.
        The exact structure of the list can be retrieved by
        :ref:`introspecting<custom-fields-instropection>` the resource.

    :>json int id: subscriber's unique identifier
    :>json datetime create_datetime: subscriber's creation datetime
    :>json int create_user: subscriber's creation :ref:`user <authentication>`'s unique identifier
    :>json datetime update_datetime: subscriber's last update datetime
    :>json int update_user: subscriber's last update :ref:`user <authentication>`'s unique identifier
    :>json string subscription: subscriber's subscription status
    :>json email email: subscriber's email
    :>json string first_name: subscriber's first name
    :>json string last_name: subscriber's last name
    :>json string gender: subscriber's gender
    :>json date date_of_birth: subscriber's date of birth
    :>json string language: subscriber's :ref:`language<languages>`
    :>json string region: subscriber's :ref:`region<regions>`

    **Request**:

    .. sourcecode:: http

        PATH /api/v1/lists/1/subscribers/1 HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json
        Content-Type: application/json

        {
            "first_name": "Altered Dolly",
        }

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: GET, PUT, PATCH, DELETE, HEAD, OPTIONS
        Content-Type: application/json

        {
            "id": 1,
            "create_datetime": "2015-11-27T22:14:36.590658Z",
            "create_user": 1,
            "update_datetime": "2015-11-28T22:14:36.590711Z",
            "update_user": 1,
            "subscription": "active",
            "email": "test@example.com",
            "first_name": "Altered Dolly",
            "last_name": "Parton",
            "gender": "f",
            "date_of_birth": "1946-01-19",
            "language": "en",
            "region": "US-TN"
        }

    :status 400: invalid subscriber data
    :status 404: no subscriber match the specified ``list_id`` and ``id``
    :status 409: a subscriber with the specified ``email`` :ref:`already exists in this list<email-conflict>`.

.. http:delete:: /api/v1/lists/(int:list_id)/subscribers/(int:id)

    Change the ``subscription`` status of the subscriber matching the provided
    ``id`` and ``list_id`` to ``deleted``.

    :param list_id: list's unique identifier
    :type list_id: int
    :param id: subscriber's unique identifier
    :type id: int

    **Request**:

    .. sourcecode:: http

        DELETE /api/v1/lists/1/subscribers/1 HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 204 NO CONTENT
        Vary: Accept
        Allow: GET, PUT, DELETE, HEAD, OPTIONS, PATCH

    :status 204: the subscriber was deleted successfully
    :status 404: no subscriber match the specified ``list_id`` and ``id``

.. _`subscription-activation`:

.. http:post:: /api/v1/lists/(int:list_id)/subscribers/(int:id)/activate

    Change the ``subscription`` status of the subscriber matching the provided
    ``id`` and ``list_id`` to either ``pending`` or ``active`` depending on
    the list's subscription process and the value of the ``confirm``
    parameter.

    :param list_id: list's unique identifier
    :type list_id: int
    :param id: subscriber's unique identifier
    :type id: int

    :<json boolean confirm: whether or not to force or disable activation confirmation

    :>json string status: the subscriber's subscription status

    .. sourcecode:: http

        POST /api/v1/lists/1/subscribers/1/activate HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: POST, OPTIONS
        Content-Type: application/json

        {
            "status": "active"
        }

    :status 400: the subscription activation cannot be confirmed since not opt-in process is configured for the specified list.
    :status 404: no subscriber match the specified ``list_id`` and ``id``

.. http:post:: /api/v1/lists/(int:list_id)/subscribers/(int:id)/unsubscribe

    Change the ``subscription`` status of the subscriber matching the provided
    ``id`` and ``list_id`` to ``unsubscribed``.

    :param list_id: list's unique identifier
    :type list_id: int
    :param id: subscriber's unique identifier
    :type id: int

    :>json string status: the subscriber's subscription status

    .. sourcecode:: http

        POST /api/v1/lists/1/subscribers/1/unsubscribe HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: POST, OPTIONS
        Content-Type: application/json

        {
            "status": "unsubscribed"
        }

    :status 404: no subscriber match the specified ``list_id`` and ``id``
