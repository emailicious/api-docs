=======
Imports
=======

.. http:post:: /api/v1/lists/(int:list_id)/imports

    Import an uploaded `CSV`_ as subscribers of the specified list.

    .. _`CSV`: https://en.wikipedia.org/wiki/Comma-separated_values

    :param list_id: list's unique identifier
    :type list_id: int

    :form file: the `CSV`_ subscriber file
    :form encoding: the file encoding, detected automatically if not specified
    :form delimiter: column delimiter, detected automatically if not specified
    :form has_header: whether or not the file has an header, detected automatically if not specified
    :form ignore_invalid_fields: whether or not rows with invalid fields should be considered or not
    :form date_format: the `strptime format`_ used to express dates
    :form fields: array mapping column indexes to fields

    .. _`strptime format`: https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior

    If the ``fields`` parameter is not specified the ``file`` must start with
    an header row mapping the file columns to the subscriber list fields and
    the ``has_header`` parameter must be set to ``true``.

    .. csv-table:: subscribers.csv
        :header: "email", "first_name", "gender", "language"

        "alice@domain.com", "Alice", "f", "fr"
        "bob@example.com", "Bob", "m", "en"

    **Request**:

    .. sourcecode:: http

        POST /api/v1/lists/1/imports HTTP/1.1
        Host: account.emailicious.com
        Accept: application/json
        Content-Type: multipart/form-data; boundary=------------------------aefc77a7a0e120e9

    **Response**:

    .. sourcecode:: http

        HTTP/1.1 201 CREATED
        Vary: Accept
        Allow: GET, POST, HEAD, OPTIONS
        Content-Type: application/json

        {
            "id": 1,
            "file": "subscribers.csv",
            "encoding": "utf-8",
            "delimiter": ",",
            "has_header": true,
            "ignore_invalid_fields": true,
            "date_format": "%d-%m-%Y",
            "fields": [
                "email",
                "first_name",
                "gender",
                "language"
            ]
        }

    :status 201: the import was created successfully
    :status 400: invalid import data
    :status 404: no subscriber list match the specified ``list_id``
