Backend Components
#########


Chatroom Manager
===============

Primarily handled in API endpoint logic, holds one function to return chatroom stats.

``return_stats(chatroom_id)``
- Returns a dict of stats for any given chatroom, ideal for displaying on the map screen.

Database Manager
===============

Handles interfacing with the PSQL database as well as first-boot DB population.

``_get_db_config()``
- Returns the config file for use in connecting to the Chatlus PSQL database.

``queryDB(sql_query)``
- Executes SQL on the database, fetches all results and returns them.

``executeOnDB(sql_query)``
- Executes SQL on the database but returns no results, ideal for POST-style functions.

``firstBoot()``
- Resets the database to the schema depicted in database_create.sql, adds test_inserts.sql as well, and runs databaseSampleGenerator() ensure equal database on first-boot.

``seedIfEmpty()``
- Populates the database with the bundled sample data only when no users exist.

``databaseSampleGenerator()``
- Generates some dummy data for testing purposes.

``databaseConnect()``
- Helper function, returns a connection, only really used by other database_connector functions.

Location Manager
===============

Handles interfacing with Google Maps Tile API, as well as caching results for faster access.

``initialiseMapAPI()``
- Creates a session key based on pre-defined parameters and API key found in /backend/.env file. Returns this key.

``returnMap(coordinates,zoom)``
- Returns image (file) if cached, fetches from Google API if not found.

``cacheMapData(coordinates,zoom)``
- Calls coordsToTile, then calls the Google Maps Tile API to get a tile with the proper parameters.

``roundCoordinates(coordinates,zoom)``
- Coordinates can be rounded when the resulting image would be equal regardless, allowing for more efficient caching.

``coordsToTile(coordinates,zoom)``
- Converts coordinates to Google API Tile Coordinates (their own projection, the code snippet is adapted from their JS example code.)

User Manager
===============

Handles user settings and manages user blocks.

``is_block_relationship_present(blocker_id,blocked_id)``
- Checks if block exists one way. Used in has_block_between_users() to check two-way block.

``has_block_between_users(user_a_id,user_b_id)``
- Runs is_block_relationship_present on both sides to check if a block exists at all.

``get_chatroom_type(chatroom_id)``
- Checks chatroom type - if it exists! Returns none if not.

``get_chatroom_member_ids(chatroom_id)``
- Gets IDs of all members in a chatroom.

``chatroom_membership_exists(chatroom_id, user_id)``
- Check if user is part of chatroom.

``get_dm_request(request_id)``
- returns a dict version of a DM request, used in the API route for accepting or rejecting requests.

``is_dm_access_accepted(chatroom_id, sender_id)``
- Check if DM is allowed to be accessed (does not check for blocks. that is the function below)

``is_blocked_dm_message(chatroom_id, sender_id)``
- Check if DM is blocked from being accessed

``set_notifications_enabled(user_id, enabled: bool)``
- Enables or disables notifications.

``get_notifications_enabled(user_id)``
- Return whether the user has chosen to enable notifications (defaults True).

``set_presence_visibility(user_id, visible: bool)``
- Persist the user's preference for showing online status to others.

``get_presence_visibility(user_id)``
- Return whether the user has chosen to show their online status (defaults True).

``set_user_online(user_id)``
- Mark user as online by setting `account_status` to 'Online' and updating timestamp.

``set_user_offline(user_id)``
- Mark user as offline by setting `account_status` to 'Offline' and updating timestamp.

``is_user_online(user_id)``
- Return True if user's `account_status` is 'Online'.

``is_presence_visible_to(viewer_id, subject_user_id)``
- Return True if subject's presence should be visible to viewer.

- Rules:
  - If subject has `show_online_status` = false -> not visible
  
  - If either party has blocked the other -> not visible
  
  - Otherwise visible

  
Validation Manager
===============

Validates changes to user profile based on Regex and rules.


  
``validateUsername(username, current_user_id=None)``
- Validates username based on regex, returns bool
  
    REGEX:  ^[A-Za-z0-9_-]{5,25}$

``validateAvatarUrl(avatar_url)``
- Validates url based on regex, returns bool

    REGEX: ^(https?://|/|\.?\./)?.+\.(png|jpe?g)$

``validateBio(bio)``
- Validates bio based on conditions, returns bool

  Conditions: Must be a string, 150 characters or less, no "<script" or other injection methods.
