General
==============

Get Endpoint
------------

Returns the endpoint for your current user's websocket connection.
The gateway returned should not be cached as the returned endpoint is based on your user id and the amount of current gateways.
Connecting to the wrong gateway will result in a redirect event.

Request
~~~~~~~

.. code-block:: http

    GET https://discordapp.com/api/gateway

Response
~~~~~~~~

.. code-block:: json

    {
    	"url":"wss://gateway-cerberus.discord.gg"
    }

The URL shown here is a common example of one. It's best to always use the URL you receive from your GET request instead of statically connecting to the URL here.



Connect
-------

After a connection to the websocket has been made, this message must be sent. If it's accepted, the server will respond with the READY event.

Message (via WebSocket)
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: json

	{
		"op": 2,
		"d": {
			"token": "aaaaaaaabbbbbbbbccccccccddddddddeeeeeeeeffffffffgggggggghh",
			"v": 3,
			"properties": {
				"$os": "Windows",
				"$browser": "Chrome",
				"$device": "",
				"$referrer":" https://discordapp.com/@me",
				"$referring_domain":"discordapp.com"
			},
			"large_threshold":100,
			"compress":true
		}
	}

Note: Only d.token, d.v and d.properties.* are required


Keepalive
---------

Keepalives must be sent every "heartbeat_interval" milliseconds, as specified by the READY and RESUMED events, or the connection will be closed.

Message (via WebSocket)
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: json

Update Status
-------------

Message
~~~~~~~

.. code-block:: json

	{
		"op": 3,
		"d": {
			"idle_since": null,
			"game_id": null
		}
	}
