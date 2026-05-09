######################
Frontend Documentation
######################

"Documents the frontend function files."

********
All
********

"Files that exist outside of the other directories."

===========================
main.dart
===========================

"Starts the app, holds the backend URL. Defaults to booting login screen."

===========================
app_session.dart
===========================

"Defines a global state for the rest of the app to reference."

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

"Clears these values."

******
Groups
******

=================
create_group.dart
=================

"Frontend page for handling group creation."

``create_group()``

- "Takes in name, description, user_id, and optionally coordinates to create a group"

====================
group_chat_list.dart
====================

"Frontend page for listing joined chat groups."

``load_chatrooms()``

- "Loads all chatrooms, keeps only group chats."

====================
group_chat_page.dart
====================

"Frontend page for a single group chat conversation."

- "Displays messages and timestamps."
- "Display member information alongside their message."
- "Supports send, edit, and delete actions."

===============
group_info.dart
===============
"Frontend page for joined-group info."

- "Displays group metadata and member list."
- "Supports profile navigation linked to member avatar and username."

==========================
group_non_member_info.dart
==========================
"Frontend group-level non-member info flow."

- "Handles viewing group details before membership."

=======================
user_chatroom_page.dart
=======================
"Frontend helper page for user/chatroom entry flows."

********
Messages
********

"Message and conversation frontend pages."

=================
dm_chat_page.dart
=================
"Frontend page for direct message conversations."

- "Displays DM messages."
- "Supports send, edit, and delete actions."

============
dm_list.dart
============
"Frontend page for listing DM and group conversations."

- "Shows conversation previews."
- "Sorts by recent activity."
- "Routes to selected conversation."

=======
dm.dart
=======
"Frontend DM routing/list helper page."

********
Services
********

"Frontend API service wrappers."

===============
api_client.dart
===============
"Shared API client wrapper for POST/GET/PUT/DELETE calls."

=======================
attachment_service.dart
=======================
"Attachment-related API calls (fetching message attachments)."

==================
auth_services.dart
==================
"Authentication-related API calls (login)."

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
