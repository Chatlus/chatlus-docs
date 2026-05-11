
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

``UpdateMessage``

  ``sender_id`` - Mandatory string

  ``content`` - Mandatory String

``Login``

  ``username`` - Mandatory string

  ``password`` - Mandatory string

``DMRequest``

  ``sender_id`` - Mandatory String

  ``recipient_id`` - Mandatory String

``FriendRequest``

  ``sender_id`` - Mandatory String

  ``receiver_id`` - Mandatory String

``MentionCreate``

  ``mentioned_user`` - Mandatory string

``ReportCreate``

  ``sender_id`` - Mandatory String

  ``report_type`` - Mandatory string

  ``content`` - Mandatory String

``CreateUser``

  ``username`` - Mandatory String

  ``password`` - Mandatory String

``UpdateUser``

  ``username`` - Optional string

  ``password_hash`` - Optional string

  ``avatar_url`` - Optional string

  ``bio`` - Optional string

  ``account_status`` - Optional string

  ``age_verified`` - Optional boolean

  ``show_online_status`` - Optional boolean

  ``notifications_enabled`` - Optional boolean

Endpoint Documentation
======================

Attachments
-----------

``/attachments/chatroom/<chatroom_id>/<message_id>``

  GET - get all attachments for message
  
  POST - add attachment to message, takes json "file_url":string as args

``/attachments/chatroom/<chatroom_id>/<message_id>/<attachment_id>``

  GET - get attachment on message
  
  PUT - edit attachment, takes JSON "file_url":string as args

  DELETE - delete attachment

Auth
----

``/auth/login``

  POST - check if valid login, takes json "username":string,"password":string as args

Blocks
------

``/blocks/<user_id>``

  GET - List of users you blocked

  POST - block someone, takes json "blocked_id":uuid as args

``/blocks/<user_id>/<blocked_id>``

  DELETE - Unblock user

``/blocks/is_blocked/<user_id>/<target_id>``

  GET - check block status, one way

Chatrooms
---------

``/chatrooms/``

  GET - Get ALL CHATROOMS

  POST - Create chatroom, takes json "chatroom_type":string,"chatroom_name":string as args


``/chatrooms/<chatroom_id>``

  GET - Get chatroom

  PUT - edit chatroom parameters, takes json "chatroom_name":string as args


``/chatrooms/<chatroom_id>/memberships``

  GET - get all members of chatroom

``/chatrooms/join``

  POST - join chatroom, takes json "user_id":uuid,"chatroom_id":uuid as args

``/chatrooms/leave``

  POST - remove user from chatroom, takes json "user_id":uuid,"chatroom_id":uuid as args

``/chatrooms/create``

  POST - Create chatroom, takes json "user_id":uuid,"name":string,"description":string, "chatroom_type":string,"members":list,"lat":float,"lng":float as args
    
    Easier to memorise endpoint for POSTing /chatrooms

``/chatrooms/user/<user_id>``

  GET - For every chatroom chatrooms user belongs to, get its details, their last message there and its timestamp

``/chatrooms/<chatroom_id>/add_member``

  POST - add member to chatroom, takes json "user_id":uuid as args

``/chatrooms/<chatroom_id>/add_member``

  POST - remove member from chatroom, takes json "user_id":uuid as args

``/chatrooms/<chatroom_id>/info``

  GET - get all metadata for chatroom

DM Requests
-----------

``/dm_requests/send``

  POST - Sends DM Request, takes json "sender_id":uuid,"recipient_id":uuid as args

``/dm_requests/incoming/<user_id>``

  GET - Get incoming DM requests for user

``/dm_requests/accept/<request_id>``

  POST - Accept DM request with ID

``/dm_requests/decline/<request_id>``

  POST - Decline DM request with ID


Friend Requests
---------------

``/friend_requests/send``

  POST - Send friend request, takes json "sender_id":uuid,"receiver_id":uuid as args

``/friend_requests/<user_id>/incoming``

  GET - Get list of incoming friend requests for user

``/friend_requests/<user_id>/outgoing``

  GET - get all outgoing, currently pending friend requests from user

``/friend_requests/<request_id>/accept``

  POST - Accept incoming friend request, send notification of acceptance, create DM chatroom if doesn't exist

``/friend_requests/<request_id>/decline``

  POST - DECLINE incoming friend request

``/friend_requests/<request_id>/cancel``

  POST - cancel outgoing friend request

``/friend_requests/status/<user_id>/<target_id>``

  GET - Check status of outgoing friend request

Map
---

``/map/login``

  GET - get map image at coordinates and zoom level, effectively an interface to map api, takes lat=float,lng=float,zoom=int as POST args

``/map/chatrooms/nearby``

  GET - Get list of locational chatrooms, takes lat=float,lng=float,radius=int as POST args

Mentions
--------

``/mentions/chatroom/<chatroom_id>/<message_id>``

  GET - get mentions included in message
  
  POST - add mention to message, takes json "mentioned_user":uuid as args

Messages
--------

``/messages/chatroom/<chatroom_id>``

  GET - get all messages in chatroom

  POST - add message to chatroom, takes json "sender_id":uuid, "content":string as args

``/messages/chatroom/<chatroom_id>/<message_id>``

  PUT - edit message at ID, takes json "content":string as args

  DELETE - delete message at ID

Notifications
-------------

``/notifications/<user_id>``

  GET - GET NOTIFICATIONS FOR USER

``/notifications/mark_read/<notification_id>``

  POST - Mark notification as read

Reports
-------

``/reports/<message_id>/reports``

  GET - get all reports for message

  POST - report message, takes json "sender_id":uuid,"report_type":string,"content":string as args

``/reports/<message_id>/<report_id>``

  GET - get individual report for message, display info

  DELETE - remove report from message

Users
-----

``/users``
  
  GET - get all users

  POST - add user to database, takes in json "username":string,"password_hash":string as args

``/users/<user_id>``

  GET- Get all info about a user stored in the users table

  PUT - edit user info - takes json "field":data as args based on table described in function

``/users/<user_id>/memberships``

  GET - get all chatroom_memberships for user

  POST - add user to chatroom - takes json "chatroom_id":uuid as args

``/users/<user_id>/friends``

  GET - get all user friends

``/users/<user_id>/notifications_enabled``

  GET - return whether or not notifications are enabled for user (setting endpoint)
  
  POST - enable/disable notifications for user - takes in json "enabled":bool as args

``/users/<user_id>/presence_visibility``

  GET - return whether or not presence status is shown for user (setting endpoint)

  POST - enable/disable presence visibility setting - takes in json "visible":bool as args

``/users/<user_id>/presence/online``

  POST - set user as online

``/users/<user_id>/presence/offline``

  POST - set user as offline
