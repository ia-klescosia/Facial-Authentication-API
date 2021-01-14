Submit ID
==================================================================

This section discusses the Submit ID API where a user uploads their Government-issued ID and then the API returns the details present in the ID.

As of this writing, the support Philippine IDs are:

* Philippine Passport (New - Issued 2018)
* Driver's License
* TIN ID
* Unified Multi-Purpose ID (UMID)
* Postal ID

.. toctree::
   :maxdepth: 2
   :caption: Contents:

How to send requests via REST API
-----------------------------------

The payload accepts an `application/json` type. Please note that each image passed in the request must be ``Base64 encoded``.

**Limits**:

* Maximum payload size of **10MB**
* Maximum integration timeout **30 seconds**

The API link will be provided by the team, below is a sample **POST** method

**Sample Request**::

	{
		"uuid": "123ABAB"
		"image": "SGVsbG8sIHRoaXMgaXMgYSBzYW1wbGUgQmFzZTY0IEVuY29kZWQgc3RyaW5nLiBTZW5kaW5nIGxvdmUgZnJvbSB0aGUgSW5mbyBBbGNoZW15IFRlYW0u"
	}

**Sample Response**::

	{
	    "statusCode": 200,
	    "headers": {
	        "Content-Type": "application/json"
	    },
	    "body": {
	        "uuid": "123ABAB",
	        "id_type": "postal identity card",
	        "full_name": "JUANA REYES DELA CRUZ",
	        "issued_by": "MNL . QE"
	    }
	}


Common error gateway response types
-----------------------------------

The table below lists the common error gateway that you may encounter. If the error isn't present in the table below, kindly contact the developer.

.. csv-table::
   :file: ./_static/gateway_responses_table.csv
   :widths: 100, 500, 600