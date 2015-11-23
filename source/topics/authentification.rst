.. _authentification:

================
Authentification
================

Accessing resources exposed through the API requires explicit authentification.

All requests must include an :http:header:`Authorization` header in order
to perform `HTTP basic access authentification`_ using an existing username
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
    Since Emailicious' usernames contain the "@" caracters which is also used
    as a `username` and `password` separator you might have to
    `percent-encode`_ it to `%40` if your client doesn't handle it for you.

.. _`percent-encode`: https://en.wikipedia.org/wiki/Percent-encoding
.. _`HTTP basic access authentification`: https://en.wikipedia.org/wiki/Basic_access_authentication