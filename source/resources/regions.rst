.. _regions:

=======
Regions
=======

.. http:get:: /api/v1/regions

    List of supported `ISO-3166-1`_ country and `ISO-3166-2`_ subdivision
    codes.

    .. _`ISO-3166`: https://fr.wikipedia.org/wiki/ISO_3166
    .. _`ISO-3166-1`: https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
    .. _`ISO-3166-2`: https://en.wikipedia.org/wiki/ISO_3166-2

    :query code: filter results by ``code``
    :query search: filter results by ``name`` and country ``name``

    :>jsonarr string code: `ISO-3166`_ code of the country or subdivision
    :>jsonarr string name: :ref:`localized<localization>` name of the country or subdivision

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

.. http:get:: /api/v1/regions/(string:code)

    Details of the region matching the specified ``code``.

    :param code: `ISO-3166`_ country or subdivision code.
    :type code: string

    :>json string code: `ISO-3166`_ code of the country or subdivision
    :>json string name: :ref:`localized<localization>` name of the country or subdivision
    :>json string country: `ISO-3166-1`_ code of the subdivision's country
    :>json array regions: `ISO-3166-2`_ codes and :ref:`localized<localization>` names of the country's subdivisions

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

