Liveness Detection
==================================================================

This section discusses the Liveness Detection API where a user uploads a video selfie and Computer Vision technology is used to detect the user's nose. The API matches the person in the video to the previously sent documents by the user. Then the API returns the percentage of similarity (if it founds a match), and all the timestamps (in milliseconds) that the tip of the nose of the person is detected inside the specified bounding box. 

.. toctree::
   :maxdepth: 2
   :caption: Contents:

How to send requests via REST API
-----------------------------------

The payload accepts an `application/json` type. 

Please note that each video passed in the request must be ``Base64 encoded``.


**Limits**:

* Maximum payload size of **10MB**
* Maximum integration timeout **30 seconds**

The API link will be provided by the team, below is a sample **POST** method

**Parameters:**
 * ``top_left`` (required) is the X and Y points of the top left corner of the bounding box (in pixels)
 * ``top_right`` (required) is the X and Y points of the top right corner of the bounding box (in pixels)
 * ``bottom_left`` (required) is the X and Y points of the bottom left corner of the bounding box (in pixels)
 * ``bottom_right`` (required) is the X and Y points of the bottom right corner of the bounding box (in pixels)
 * ``uuid`` (required) is a unique ID per user
 * ``threshold`` (optional) is a value compared to the Similarity percentage (default = 80)
 * ``video`` (required) is a Base64 encoded video string

**Sample Request**::

	{	
		"top_left": {
		    "X": "262.2641706466675",
		    "Y": "761.1293792724609"
		  },
		"top_right": {
		    "X": "462.2641706466675",
		    "Y": "761.1293792724609"
		  },
		"bottom_left": {
		    "X": "262.2641706466675",
		    "Y": "561.1293792724609"
		  },
		"bottom_right": {
		    "X": "462.2641706466675",
		    "Y": "561.1293792724609"
		  },
		"uuid": "123ABAB",
		"threshold": "80"
		"video": "SGVsbG8sIHRoaXMgaXMgYSBzYW1wbGUgQmFzZTY0IEVuY29kZWQgc3RyaW5nLiBTZW5kaW5nIGxvdmUgZnJvbSB0aGUgSW5mbyBBbGNoZW15IFRlYW0u"
	}

**Sample Response**::

	{
   		"statusCode": 200,
	    "headers": {
	        "Content-Type": "application/json"
	    },
	    "body": {
	        "Match": "Yes",
	        "Similarity Rating": 99.99989318847656,
	        "LivenessDetection": "Success",
	        "Timestamps": [
	            0,
	            482,
	            999,
	            1482,
	            1999,
	            2482
	        ],
	        "X_Nose": [
            	362.2641706466675,
            	362.5665092468262,
            	364.0458869934082,
            	365.17001152038574,
            	377.46864795684814,
            	376.52305126190186
        	],
        	"Y_Nose": [
            	661.1293792724609,
            	654.8637390136719,
            	649.2276763916016,
            	648.3708953857422,
            	606.0959625244141,
            	620.4314422607422
        	],
	        "VideoMetadata": {
	            "FrameHeight": 1280,
	            "FrameWidth": 720
	        }
	    }
	}

**Note:** 

The Liveness Detection API will first check if the person in the video matches the photo in the Government ID and the image selfie. Once this is satisfied, it will proceed to detecting the tip of the nose. In the background, the API creates a small bounding box around the tip of the nose. Then each point of this small bounding box is compared to the points of the larger one (specified by application).

For the API to flag **"Match"** as **"Yes"**, the Similarity Rating must be greater than the specified threshold (default is **80**).

For the API to flag **"Liveness Detection"** as **"Success"**, the tip of the nose of the user must appear inside the specified bounding box for atleast **4 timestamps** or **2 seconds**. Kindly contact the developers if tweaking is needed for this specific criteria. 


Common error gateway response types
-----------------------------------

The table below lists the common error gateway that you may encounter. If the error isn't present in the table below, kindly contact the developer.

.. csv-table::
   :file: ./_static/gateway_responses_table.csv
   :widths: 500, 500, 600

.. rubric:: Footnotes
.. [#f1] Text of the first footnote.