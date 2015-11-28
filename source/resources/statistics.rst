==========
Statistics
==========


.. http:get:: /api/v1/statistics/opens

    List all opens statistics

    :query int campaign: filter results by campaign's unique identifier
    :query int mailing: filter results by mailing's unique identifier
    :query boolean unique: aggregate the opens by delivery
    :query date date: filter results by date
    :query datetime from_datetime: filter out results with a more recent datetime
    :query datetime to_datetime: filter out results with a less recent datetime

    :>json int mailing: the open's mailing
    :>json email email: the open's email
    :>json datetime datetime: the open's datetime

    **Request**:

    .. sourcecode:: http

        GET /api/v1/statistics/opens HTTP/1.1
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
                    "mailing": 1,
                    "email": "foo@bar.org",
                    "datetime": "2014-06-06T20:56:57Z"
                }
            ]
        }

.. http:get:: /api/v1/statistics/clicks

    List all clicks statistics

    :query int campaign: filter results by campaign's unique identifier
    :query int mailing: filter results by mailing's unique identifier
    :query boolean unique: aggregate the clicks by delivery
    :query date date: filter results by date
    :query datetime from_datetime: filter out results with a more recent datetime
    :query datetime to_datetime: filter out results with a less recent datetime
    :query url url: filter results by link URL

    :>json int mailing: the click's mailing
    :>json email email: the click's email
    :>json datetime datetime: the click's datetime
    :>json url url: the click's link URL

    **Request**:

    .. sourcecode:: http

        GET /api/v1/statistics/clicks HTTP/1.1
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
                    "mailing": 1,
                    "email": "foo@bar.org",
                    "datetime": "2014-06-06T20:56:57Z",
                    "url": "https://example.com"
                }
            ]
        }

.. http:get:: /api/v1/statistics/bounces

    List all bounces statistics

    :query int campaign: filter results by campaign's unique identifier
    :query int mailing: filter results by mailing's unique identifier
    :query boolean unique: aggregate the bounces by delivery
    :query date date: filter results by date
    :query datetime from_datetime: filter out results with a more recent datetime
    :query datetime to_datetime: filter out results with a less recent datetime
    :query boolean hard: filter result by bounce permanent status

    :>json int mailing: the bounce's mailing
    :>json email email: the bounce's email
    :>json datetime datetime: the bounce's datetime
    :>json boolean hard: the bounce's permanent status

    **Request**:

    .. sourcecode:: http

        GET /api/v1/statistics/bounces HTTP/1.1
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
                    "mailing": 1,
                    "email": "foo@bar.org",
                    "datetime": "2014-06-06T20:56:57Z",
                    "hard": false
                }
            ]
        }
