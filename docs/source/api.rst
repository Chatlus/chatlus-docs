
API Usage
#########

1. Start the backend server with ``flask run``.
2. Access the endpoints by calling them with the appropriate endpoints

API Description
===============

The backend facilitates communication with the Google Maps API as well as handling all storage and replication of user-generated content (chatrooms, messages, etc.)


Model Documentation
======================


Mandates input at endpoints, raises error if these structures are not followed.

``CreateAttachment``

  ``file_url`` - Mandatory string

``UpdateAttachment``

  ``file_url`` - Optional string

``CreateChatroom``

  ``chatroom_type`` - Mandatory string

  ``chatroom_name`` - Mandatory string

  ``coords_bottom_right`` - Optional string

  ``coords_top_left`` - Optional string

``UpdateChatroom``

  ``chatroom_name`` - Optional string

``CreateMessage``

  ``sender_id`` - Mandatory string

  ``content`` - Mandatory string

Endpoint Documentation
======================

Users
-----

``/users``

  GET - returns all users, really only good for admin purposes
  
  POST - Add a new user to the database.

``/users/<user_id>``

  GET - returns user data
  
  PUT - edit user data

Chatrooms
---------

``/chatrooms``

  GET - returns all chatrooms
  
  POST - create chatroom

``/chatroom/<chatroom_id>``

  GET - get chatroom with ID
  
  PUT - edit chatroom with ID

``/chatroom/<chatroom_id>/activity``

  GET - get chatroom activity

Messages
--------

``/chatroom/<chatroom_id>/messages``

  GET - get chatroom messages
  
  POST - add nessage to chatroom

``/chatroom/<chatroom_id>/<message_id>``
  
  GET - returns message
  
  PUT - edit message
  
  DELETE - delete message

``/chatroom/<chatroom_id>/<message_id>/attachments``

  GET - get attachments in message

  PUT - add attachments to message

``/chatroom/<chatroom_id>/<message_id>/mentions``

  GET - mentions in a message

  POST - add message mention

``/chatroom/<uuid:chatroom_id>/<message_id>/<attachment_id>``

  GET - get attachment

  PUT - edit attachment

  DELETE - delete attachment

Reports
-------

``/chatroom/<chatroom_id>/<message_id>/reports``

  GET - get reports on a message

  POST - report message

``/chatroom/<chatroom_id>/<message_id>/<report_id>``
  
  GET - get report info

  DELETE - delete report

Memberships
-----------

``/user/<user_id>/memberships``

  GET - returns user chatroom memberships

  POST - adds chatroom membership for user

``/chatroom/<chatroom_id>/memberships``

  GET - get chatroom members

Relationships
-------------

``/user/<user_id>/requests``

  GET - returns all DM requests a user has been sent
  
  POST - send a DM request to this user

``/user/<user_id>/requests/<request_id>/accept``

  POST - user accepts the DM request.

``/user/<user_id>/requests/<request_id>/reject``

  POST - user rejects the DM request.

Blocks
------

``/blocks/<user_id>``

  GET - Returns user blocks

  POST - blocks new user

``blocks/<user_id>/<blocked_id>``

  DELETE - Unblocks user

``/is_blocked/<user_id>/<target_id>

  GET - Check if target is blocked by user

Map
---

``/map``

  GET request with lat,long and zoom coordinates will return a png from the Google Maps Tile API or temporary server-side cache respectively.
