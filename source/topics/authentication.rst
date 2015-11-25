.. _authentication:

==============
Authentication
==============

Accessing resources exposed through the API requires explicit authentication.

All requests must include an :http:header:`Authorization` header in order
to perform `HTTP basic access authentication`_ using an existing username
and password as credentials.

.. sourcecode:: http

    GET /api/v1 HTTP/1.1
    Host: account.emailicious.com
    Authorization: Basic Zm9vOmJhcg==

Failing to provide valid credentials will result in an :http:statuscode:`401`
response.

.. sourcecode:: http

    HTTP/1.1 401 UNAUTHORIZED
    Content-Type: application/json
    WWW-Authenticate: Basic realm="api"

    {
        "detail": "Invalid username/password."
    }

.. note::
    Emailicious usernames contain the "@" character which is also used as the
    `credential` and `host` separator of an `URI`_. Most HTTP clients make
    sure to `percent-encode`_ the `username` and `password` part but you might
    have to replace this character by `%40` if it's not the case.

    For example, the `cURL`_ command line tool requires manual replacement::

        curl https://user%40domain.com:password@account.emailicious.com/api/v1

.. _`HTTP basic access authentication`: https://en.wikipedia.org/wiki/Basic_access_authentication
.. _`URI`: https://en.wikipedia.org/wiki/Uniform_Resource_Identifier#Syntax
.. _`percent-encode`: https://en.wikipedia.org/wiki/Percent-encoding
.. _`cURL`: http://curl.haxx.se/
