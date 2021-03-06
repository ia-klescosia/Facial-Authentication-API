Submit ID
==================================================================

This section discusses the Submit ID API where a user uploads their Government-issued ID and then the API returns the details as well as the image present in the ID.


As of this writing, the supported Philippine IDs are:

* Philippine Passport (New - Issued 2018) [#f1]_
* Driver's License
* TIN ID
* Unified Multi-Purpose ID (UMID)
* Postal ID

.. toctree::
   :maxdepth: 2
   :caption: Contents:

How to send POST requests via REST API
---------------------------------------

API: https://6sdo4wx835.execute-api.ap-southeast-1.amazonaws.com/dev/submitid

The payload accepts an `application/json` type. 

Please note that each image passed in the request must be ``Base64 encoded``.


**Limits**:

* Maximum payload size of **10MB**
* Maximum integration timeout **30 seconds**

The API link will be provided by the team, below is a sample **POST** method

**Parameters:**
 * ``uuid`` (required) is a unique ID per user
 * ``image`` (required) is a Base64 encoded image string

**Sample Request** 

.. code-block:: JSON

	{
		"uuid": "123ABAB",
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
			"uuid": "123ABAB",
			"id_type": "postal identity card",
			"full_name": "JUANA REYES DELA CRUZ",
			"issued_by": "MNL . QE"
		}
	}

**Note:** 

The Submit ID API, in most cases, will detect the text in the image and will search all the fields and will load them into their respective fields. 
In case some of the fields in the API's response is missing, here are some troubleshooting steps that you can take:

* The Submit ID API relies on the quality of the image provided, as such, the captured image should not contain any glare, reflection or shadows
* Crop the image to the ID's size to make it more reliable
* The users may also lower the camera resolution by changing their phone's camera settings
* If all else fails, kindly notify the developers to troubleshoot and debug (please indicate the problems encountered, thank you!)


How to send GET requests via REST API
--------------------------------------

API: https://6sdo4wx835.execute-api.ap-southeast-1.amazonaws.com/dev/getdetails

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
		"uuid": "123ABAB",
		"id_type": "postal identity card",
		"full_name": "JUANA REYES DELA CRUZ",
		"issued_by": "MNL . QE"
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


.. rubric:: Footnotes
.. [#f1] Text of the first footnote.