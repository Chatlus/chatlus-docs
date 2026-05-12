######################
Frontend Documentation
######################

Documents the frontend function files.

********
All
********

Files that exist outside of the other directories.

===========================
main.dart
===========================

Starts the app, holds the backend URL. Defaults to booting login screen.

``main()`` - Runs app with class ConnectApp()

``ConnectApp`` - contains widget that builds login screen.

===========================
app_session.dart
===========================

Defines a global state for the rest of the app to reference.

``currentUserId``

``currentUsername``

``currentAvatarUrl``

``currentUserId``

``currentUsername``

``currentAvatarUrl``

Dev Variables
^^^^^^^^^^^^^

``isOfflineDevMode``

``localAvatarUrl``

``localBio``



``clear()``

Clears these values.

******
Groups
******

=================
create_group.dart
=================

Frontend page for handling group creation.

``create_group()`` - Takes in name, description, user_id, and optionally coordinates to create a group using ChatroomService

``CreateGroupPage`` - takes in lat,lng, userID

====================
group_chat_list.dart
====================

Frontend page for listing joined chat groups.

``load_chatrooms()`` - Loads all chatrooms, keeps only group chats.

``GroupChatsList`` - takes in userId

====================
group_chat_page.dart
====================

Frontend page for a single group chat conversation.

- Displays messages and timestamps.
- Display member information alongside their message.
- Supports send, edit, and delete actions.

``formatTime()`` - takes in raw datetime string, return in format hours:minutes (HH:MM)

``loadMessages()`` - Calls MessageService equivalent.

``_scrollToBottom()`` - jumps to bottom of page, called on message load

``_sendMessage()`` - calls MessageService equivalent

``_isMe()`` - returns bool if signed-in user ID matches message user ID

``_showEditDialog()`` - shows widget asynchronously

``_handleAvatarTap()`` - opens profile if not friends, opens DM if friends

``_buildMessages()`` - for every message, creates widget to display

``GroupChatPage`` - takes in chatroom ID, group name, user ID

===============
group_info.dart
===============

Frontend page for joined-group info.

- Displays group metadata and member list.
- Supports profile navigation linked to member avatar and username.

``loadInfo()`` - calls ChatroomService equivalent

``GroupInfoPage`` - takes in chatroom ID, user ID

==========================
group_non_member_info.dart
==========================

Frontend group-level non-member info flow.

- Handles viewing group details before membership.

``loadGroupInfo()`` - calls ChatroomService equivalent

``joinGroup()`` - calls ChatroomService equivalent

``GroupInfoPAgeNonMember`` - takes in groupName, chatroom ID, user ID

=======================
user_chatroom_page.dart
=======================

Frontend helper page for user/chatroom entry flows.

``loadChatrooms()`` - calls CHatroomSerice equivalent

``GroupsPageScreen`` - takes in User ID

********
Messages
********

Message and conversation frontend pages.

=================
dm_chat_page.dart
=================

Frontend page for direct message conversations.

- Displays DM messages.
- Supports send, edit, and delete actions.

``_loadFriendAvatar()`` - calls userService equivalent

``formatTime()`` - takes in raw datetime string, return in format hours:minutes (HH:MM)

``loadMessages()`` - Calls MessageService equivalent.

``_scrollToBottom()`` - jumps to bottom of page, called on message load

``_sendMessage()`` - calls MessageService equivalent

``_isMe()`` - returns bool if signed-in user ID matches message user ID

``_showEditDialog()`` - shows widget asynchronously

``_handleAvatarTap()`` - opens profile if not friends, opens DM if friends

``_buildMessages()`` - for every message, creates widget to display

``DMChatPage`` - takes in chatroom ID, user ID, friend ID, friend Username

============
dm_list.dart
============

Frontend page for listing DM and group conversations.

- Shows conversation previews.
- Sorts by recent activity.
- Routes to selected conversation.

``loadChatrooms()`` - calls ChatroomService equivalent

``MessagesPageScreen`` - takes in User ID

=======
dm.dart
=======

Frontend DM routing/list helper page.

``loadChatrooms()`` - calls ChatroomService equivalent

********
Services
********

Frontend API service wrappers.

===============
api_client.dart
===============

Shared API client wrapper for POST/GET/PUT/DELETE calls.

``post()`` - takes in endpoint, data, posts the url

``get()`` - takes in endpoint, gets the url

``put()`` - takes in endpoint and data, puts data at endpoint

``delete()`` - takes in endpoint, deletes at url

=======================
attachment_service.dart
=======================

Attachment-related API calls (fetching message attachments).

``getAttachments()`` - takes in chatroom ID, message ID, gets List of attachments for message

==================
auth_services.dart
==================

Authentication-related API calls (login).

``login()`` - takes in username, password, returns data at user_id

===================
block_services.dart
===================
"Blocking-related API calls (block/unblock/list blocked users)."

=======================
chatrooms_services.dart
=======================
"Chatroom-related API calls (list/create/join/leave/nearby/info)."

========================
dm_request_services.dart
========================
"Direct-message-request API calls (send/list/respond)."

===========================
friend_request_services.dart
"Friend-request API calls (send/list/status/accept/decline)."

=====================
friends_services.dart
=====================
"Friends API calls (friend list and related friend actions)."

=====================
message_services.dart
=====================
"Message API calls (load/send/edit/delete)."

==========================
notification_services.dart
==========================
"Notification API calls (load and notification state actions)."

=================
user_service.dart
=================
"User profile API calls (user fetch, avatar/bio updates, presence fetch)."

*****
Theme
*****

===============
app_colour.dart
===============
"Shared colour tokens/constants."

================
app_spacing.dart
================
"Shared spacing tokens/constants."

===================
app_text_style.dart
===================
"Shared text style tokens/constants."

==============
app_theme.dart
==============
"Global app ThemeData configuration."
