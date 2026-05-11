Developer Guide
===============

.. _backend:
Backend
-------

^^^^^^^^^^^^^
Install Guide
^^^^^^^^^^^^^

1. Install the latest version of Python.
2. Install PSQL and ensure that you can enter commands. Run ``CREATE USER chatlus;CREATE DATABASE app;`` in the PSQL terminal.
  You also need to give the ``chatlus`` user the necessary permissions on database ``app``, namely creating tables, inserting data and managing the schema. As you are granting permissions on a dev environment where only the backend can access the database, ``GRANT ALL ON DATABASE app TO chatlus;`` should suffice. More granular permissions should be granted in a production environment.
3. Clone the Git repo and run `cd backend` in your preferred code editor.
4. Run ``pip install -r requirements.txt`` to get the required dependencies installed (likely requires a venv folder to install correctly.)
5. To enable the map feature, you need an API key for Google Map Tile API. Generate this with a Google account.
6. Create a file named ``.env`` in ``/backend``, and enter GOOGLE_MAPS_API_KEY=[YOUR API KEY] in it.
  Some users have reported an issue where the environment key will not read unless the encoding of ``.env`` is ``UTF-8``. Ensure this is the case if it does not work.

^^^^^^^^^^^^^
Usage Guide
^^^^^^^^^^^^^

By default, the API can be accessed at http://127.0.0.1:5000/<api_route>.

1. Clone the Git repo and run `cd backend` in your preferred code editor.
2. Run `flask run` to start the backend server.

^^^^^^^^^^^^^
Components
^^^^^^^^^^^^^
- Database: PSQL server
- Database Connector: Python script that connects the PSQL database to the rest of the backend.
- Location Manager: Python script that interfaces with the Location API to pull map data and push it to the frontend.
- User Manager: Python script that manages distributing and storing updates to users.
- Chatroom Manager: Python script that manages distributing and storing updates to chatrooms.
- User Validator: Python script that ensures users have permissions to access any particular resources (chatrooms, profiles, etc.)


.. _frontend:
Frontend
--------

Technologies are currently Dart and Flutter, as well as Android Studio Goes in ``/frontend/``

^^^^^^^^^^^^^
Prerequisites
^^^^^^^^^^^^^

- Flutter (2.1GB)
- Android Studio (1.4GB) + SDK (2.4GB) (And more.)

^^^^^^^^^^^^^
Install Guide
^^^^^^^^^^^^^

1. Install Flutter as described here: https://docs.flutter.dev/install/quick
2. Install Android Studio as described here: https://developer.android.com/studio/install
3. Set it up for use with Flutter as described here: https://docs.flutter.dev/platform-integration/android/setup

^^^^^^^^^^^^^
Test Instructions
^^^^^^^^^^^^^

1. Pull this repository and open it with your preferred Code Editor
2. Run ``cd frontend`` in the terminal.
3. Setup your device for use with Flutter:

* Run ``flutter emulators --launch [Emulator_Name]`` to launch your Android Emulator, if applicable.

4. Run ``flutter run`` in the terminal to open your Android Emulator/Device and run the app.

^^^^^^^^^^^^^
Build Instructions
^^^^^^^^^^^^^

1. Pull this repository and open it with your preferred Code Editor
2. Run ``cd frontend`` in the terminal.
3. Run ``flutter build`` in the terminal to compile app.



.. _goals:
Developer Goals
---------------
Scope of the project is to produce an application (and accompanying backend) that covers all possible User and System requirements as listed in Coursework Item 1.

.. _tips:
Helpful Tips
------------
The 'theme' folder contains the Chatlus app colours, font styles, padding and spacing presets for easy and consistent styling.


