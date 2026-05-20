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

Blocking-related API calls (block/unblock/list blocked users).

``blockUser()`` - takes in user ID (of blocker) and target ID (of blocked), blocks user

``unblockUser()`` - takes in user ID (of blocker) and target ID (of blocked), unblocks user

``isBlocked()`` - takes in user ID (of blocker) and target ID (of blocked), returns True if is_blocked returns True on backend

``getBlockedUsers()`` - takes in User ID, returns list of users blocked by user

=======================
chatrooms_services.dart
=======================

Chatroom-related API calls (list/create/join/leave/nearby/info).

``getNearbyGroups()`` - takes in lat,long,radius, returns nearby chatrooms list from backend

``joinChatroom()`` - takes in userID, chatroom ID, posts backend join functionality

``getChatroomInfo()`` - takes in Chatroom ID and optionally viewer ID, returns chatroom info from backend

``leaveChatroom()`` - takes in userId, chatroomId, posts backend leave functionality

``getChatroomMembers()`` - takes in chatroom ID, returns list of memberships from backend

``getUserChatrooms()`` - takes in user ID, returns list of chatrooms user is in from backend

``createDM()`` - Takes in User ID, Friend's User ID, Friend's Username, creates a DM by posting backend

``getNearbyChatroom()`` - Takes in coordinates, returns list of nearby chatrooms from backend

``createLocationGroup()`` - Takes in UserID, name, description, coordinates, posts create locational group functionality on backend

``addMember()`` - Takes in Chatroom ID, User ID, posts add_member on backend

========================
dm_request_services.dart
========================

Direct-message-request API calls (send/list/respond).


``sendDMRequest()`` - takes in two user IDs (sender and recipient), sends a DM request through backend

``getIncomingRequests()`` - takes in userID, returns list of incoming DM requests for user

``acceptRequest()`` - Takes in requestID,  accepts incoming DM request

``decineRequest()`` - Takes in requestID,  declines incoming DM request

============================
friend_request_services.dart
============================

Friend-request API calls (send/list/status/accept/decline).

``sendRequest()`` - takes in two user IDs (sender and recipient), sends a request through backend

``acceptRequest()`` - Takes in requestID,  accepts incoming request

``decineRequest()`` - Takes in requestID,  declines incoming request

``cancelRequest()`` - Takes in requestID,  cancels outgoing request

``getIncomingRequests()`` - takes in userID, returns list of incoming friend requests for user

``getOutgoingRequests()`` - takes in userID, returns list of outgoing friend requests from user

``getStatus()`` - Takes in UserID, TargetID, returns status of ongoing friend request.

=====================
friends_services.dart
=====================
"Friends API calls (friend list and related friend actions)."

``getFriends()`` - takes in user ID, returns user friend list

``unfriend()`` - takes in user ID + target user ID, removes friend on backend

``blockUser()`` - takes in User ID + Target User ID as well as Block bool, either blocks or unblocks target respectively

``reportUser()`` - Takes in user ID + Target User ID, reports user on backend

``isFriend()`` - Takes in User ID + Target ID, returns bool if user friend on backend

``getUserProfile()`` - takes in Target User ID, returns user data from backend

=====================
message_services.dart
=====================

Message API calls (load/send/edit/delete).

``getMessages()`` - takes in chatroomID, optionally userID (for more info), returns messages for any chatroom regardless of type

``sendMessage()`` - takes in chatroomID, senderID, content, sends message to any chatroom regardless of type

``editMessage()`` - takes in ChatroomID, messageID, and new message (to replace old message), replaces message

``deleteMessage()`` - takes in chatroomID, messageID, deletes message

==========================
notification_services.dart
==========================

Notification API calls (load and notification state actions).

``getNotifications()`` - takes in UserID, returns notifications for user from backend

``markAsRead()`` - takes in Notification ID, marks notification as read on backend

=================
user_service.dart
=================

User profile API calls (user fetch, avatar/bio updates, presence fetch).

``getUser()`` - takes in UserID, returns user data

``getUserWithPresence()`` - Takes in UserID, viewerID (for more info), returns user object with presence info

``updateBio()`` - takes in UserID, new bio, replaces bio contents on backend

``updateAvatarUrl()`` - takes in UserID, new avatar url, replaces URL on backend

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


*****
Views
*****

User-facing screens that primarily handle widgets, but have some code functionality. Only files with code will be listed for brevity's sake.

=================
blocked_user.dart
=================

``LoadBlocked()`` - calls BlockService for blocked users

=================
dm_request.dart
=================

``loadCandidates()`` - runs on page start, loads all friends and chatroom members from FriendService and ChatroomService equivalents

``sendInvite()`` - calls ChatroomService equivalent

===================
friend_list.dart
===================

``loadFriends()`` - calls FriendService equivalent.

===================
friend_profile.dart
===================

``loadPresence()`` - Gets info about friend user with presence data from UserService

``loadBlockStatus()`` - calls BlockService equivalent

``loadSharedData()`` - If not blocked, create a DM chatroom, load messages and accompanying data

===================
home_page_screen.dart
===================

``_determinePosition()`` - uses Geolocator API to return lat,lng coordinates

``fetchNearbyGroups()`` - calls _determinePosition, uses this to getNearbyGroups with ChatroomService equivalent

======================
login_page_screen.dart
======================

``login()`` - Takes in username and password from text boxes, checks validity, uses AuthService equivalent function to validate login

======================
map_area.dart
======================

``loadMap()`` - loads map image from  backend

======================
map_screen.dart
======================

``_determinePosition()`` - uses Geolocator API to return lat,lng coordinates

``setLocation()`` - sets state to lat,lng coordinates

=======================
navigation_screen.dart
=======================

``didChangeAppLifecycleState()`` - Mark user presence as offline if the app idles

``hasRemoteAvatar()`` - return bool if avatarUrl isn't null and starts with a http:// or https://

``_loadCurrentUserAvatar()`` - gets current user's avatar

``_openProfile()`` - Pushes to profile screen

=======================
non_friend_page.dart
=======================

``loadData()`` - loads all relevant data for a profile (friendship status, profile,block status, status of DM requests)

``sendFriendRequest()`` - calls FriendRequestService equivalent

``acceptRequest()`` - calls FriendRequestService equivalent

``declineRequest()`` - calls FriendRequestService equivalent

``sendDMRequest()`` - calls DMRequestService equivalent

``toggleBlock()`` - calls BlockService equivalent

``reportUser()`` - calls FriendService equivalent

``openDM()`` - opens DMChatPage using ChatroomService equivalent info

========================
non_member_group.dart
========================

``loadGroupInfo()`` - calls ChatroomService equivalent

``joinGroup()`` - calls ChatroomService equivalent

=========================
notification_page_screen.dart
=========================

``loadNotifications()`` - Calls NotificationService equivalent

``_buildSummaryGroups()`` - For each notification, use them to build a grouped notification, then construct a summary notification

``_formatDayLabel()`` - take a datetime and convert it to Today/Yesterday or add months.

``_iconForNotificationType()`` - Return correct icon for notification type

``handleNavigation()`` - On notification click, push to appropriate page, mark notif as read

===========================
notification_settings_screen.dart
===========================

``_setVisibility()`` - takes in boolean, sets setting on backend

``_loadVisibility()`` - loads setting from backend

===========================
privacy_settings_screen.dart
===========================

``_setVisibility()`` - takes in boolean, sets setting on backend

``_loadVisibility()`` - loads setting from backend

===========================
profile_page_screen.dart
===========================

``loadUser()`` - loads all user data (with presence) and formats it

``saveBio()`` - updates bio on backend with UserService equivalent

``saveAvatarUrl()`` - updates avatar url on backend with UserService equivalent

``editAvatarUrl()`` - Takes in value for avatar URL

``_buildAvatar()`` - Creates CircleAvatar from avatarUrl
