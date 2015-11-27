======
Errors
======

*************
Client errors
*************

When an HTTP request to the API is malformed a response with a ``4XX`` status
code is returned.

:http:statuscode:`400`
----------------------

The request is invalid. If you attempted to modify or create a resource it's
possible the request body contains invalid data (e.g. a required field is
missing, an email field is invalid, ...). The response body should contain
more details about the origins of the error.

:http:statuscode:`401`
----------------------

The provided credentials are invalid. Refer to the
:ref:`authentication<authentication>` section for troubleshooting.

:http:statuscode:`404`
----------------------

The specified resource doesn't exist or is not accessible anymore. You should
make sure the specified `URI`_ is valid.

.. _`URI`: https://en.wikipedia.org/wiki/URI

:http:statuscode:`409`
----------------------

The alteration of the specified resource is conflictual. More details should
be available from the response body and a conflict resolution strategy should be
detailed in the specified :ref:`resource<resources>` documentation.

*************
Server errors
*************

When Emailicious' servers cannot treat your request adequately a response with
a ``5XX`` status code is returned. Such instances should be rare and
intermittent and you should contact our `support team`_ if the problem
persists.

.. _`support team`: support@emailicious.com

:http:statuscode:`500`
----------------------

Emailicious' servers encountered an undisclosed internal error processing
your request and our engineers are working toward fixing the underlying issue.
The response should contain an :http:header:`X-Sentry-ID` header containing a
`UUID`_ identifying your request that might be requested by Emailicious'
`support team`_.

.. _`UUID`: https://en.wikipedia.org/wiki/Universally_unique_identifier
