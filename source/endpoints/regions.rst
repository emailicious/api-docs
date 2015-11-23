=======
Regions
=======

.. http:get:: /api/v1/languages

    List of supported `ISO-3166-1 country codes`_ and
    `ISO-3166-2 country subdivision codes`_.

    .. _`ISO-3166-1 country codes`: https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
    .. _`ISO-3166-2 country subdivision codes`: https://en.wikipedia.org/wiki/ISO_3166-2

    :query code: filter results by ``code``.
    :query search: filter results by ``name`` and country ``name``.

    **Request**:

    .. sourcecode:: http

        GET /api/v1/regions HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: GET, HEAD, OPTIONS
        Content-Type: application/json
        
        {
            "count": 5140,
            "next": "/api/v1/regions?page=2",
            "previous": null,
            "results": [
                {
                    "code": "AD",
                    "name": "Andorra"
                },
                {
                    "code": "AD-02",
                    "name": "Canillo"
                },
                {
                    "code": "AD-03",
                    "name": "Encamp"
                },
                {
                    "code": "AD-04",
                    "name": "La Massana"
                },
                {
                    "code": "AD-05",
                    "name": "Ordino"
                }
            ]
        }

.. http:get:: /api/v1/languages/(code)

    Details of the region matching the specified ``code``.

    :param code: `ISO-3166` country or subdivision code.

    **Request**:

    .. sourcecode:: http

        GET /api/v1/regions/CA HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 200 OK
        Vary: Accept
        Allow: GET, HEAD, OPTIONS
        Content-Type: application/json
        
        {
            "code": "CA",
            "name": "Canada",
            "country": null,
            "regions": [
                {
                    "code": "CA-AB",
                    "name": "Alberta"
                },
                {
                    "code": "CA-BC",
                    "name": "British Columbia"
                },
                {
                    "code": "CA-MB",
                    "name": "Manitoba"
                },
                {
                    "code": "CA-NB",
                    "name": "New Brunswick"
                },
                {
                    "code": "CA-NL",
                    "name": "Newfoundland and Labrador"
                },
                {
                    "code": "CA-NS",
                    "name": "Nova Scotia"
                },
                {
                    "code": "CA-NT",
                    "name": "Northwest Territories"
                },
                {
                    "code": "CA-NU",
                    "name": "Nunavut"
                },
                {
                    "code": "CA-ON",
                    "name": "Ontario"
                },
                {
                    "code": "CA-PE",
                    "name": "Prince Edward Island"
                },
                {
                    "code": "CA-QC",
                    "name": "Quebec"
                },
                {
                    "code": "CA-SK",
                    "name": "Saskatchewan"
                },
                {
                    "code": "CA-YT",
                    "name": "Yukon Territory"
                }
            ]
        }

