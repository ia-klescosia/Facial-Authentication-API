Selfie Match
==================================================================

This section discusses the Selfie Match API where the application takes in a Selfie image of the person and then matching it with the Government ID that was provided in the Submit ID API.

How it works
-----------------------------------

The application captures an image and encodes it to a ``Base64 encoded`` string, then calls the ``selfie match`` API which is powered by a Amazon's Facial-Recognition AI, it then validates image to the Government Issued ID.

How to send POST requests via REST API
---------------------------------------

API: https://6sdo4wx835.execute-api.ap-southeast-1.amazonaws.com/dev/selfieapi

The payload accepts an `application/json` type. 

Please note that each image passed in the request must be ``Base64 encoded``.

**Limits**:

* Maximum payload size of **10MB**
* Maximum integration timeout **30 seconds**

The API link will be provided by the team, below is a sample **POST** method

**Parameters:**
 * ``uuid`` (required) is a unique ID per user
 * ``threshold`` (optional) is the confidence level for the matched image
 * ``image`` (required) is a Base64 encoded image string

**Sample Request**

.. code-block:: JSON
	
	{
		"uuid": "123ABAB",
		"threshold": "80",
		"image": "SGVsbG8sIHRoaXMgaXMgYSBzYW1wbGUgQmFzZTY0IEVuY29kZWQgc3RyaW5nLiBTZW5kaW5nIGxvdmUgZnJvbSB0aGUgSW5mbyBBbGNoZW15IFRlYW0u"
	}

**Sample Response**

.. code-block:: JSON

	{
		"statusCode": 200,
		"headers": {
			"Content-Type": "application/json"
		},
		"body": {
			"Match": "Yes",
			"Similarity Rating": 100.0,
			"Collection ID": "123ABAB"
		}
	}

How to send GET requests via REST API
--------------------------------------

API: https://6sdo4wx835.execute-api.ap-southeast-1.amazonaws.com/dev/getselfie

The API allows sending `GET` requests in an event that there is a failed network connectivity in the client side.

This will allow the application to bypass the process of having to `POST` data all over again which will result in having a higher cost.

**Sample Request** 

.. code-block:: JSON

	{
		"uuid": "123ABAB"
	}

**Sample Response**

.. code-block:: JSON

	{
		"statusCode": 200,
		"headers": {
			"Content-Type": "application/json"
		},
		"body": {
			"Match": "Yes",
			"Similarity Rating": 100.0,
			"Collection ID": "123ABAB"
		}
	}

**Note:** 

The `GET` API allows only a maximum of **5 retries**. If this limit is reached, an error response would be returned instead.

.. code-block:: JSON
	
	{
		"statusCode": 500,
		"headers": {
			"Content-Type": "application/json"
		},
		"body": "Number of maximum tries has been reached. Please try again later. Or contact the developer"
	}


Common error gateway response types
-----------------------------------

The table below lists the common error gateway that you may encounter. If the error isn't present in the table below, kindly contact the developer.

.. csv-table::
   :file: ./_static/gateway_responses_table.csv
   :widths: 500, 500, 600
