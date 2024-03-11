#   Imports:
        Flask and related modules for building the web application.
        Flask-MySQL for connecting to a MySQL database.
        Flask-Hashing for password hashing.
        Flask-Login for user authentication.
#   Database Configuration:

        The code retrieves database credentials (username, password, hostname, port, etc.) from environment variables.
        A MySQL connection pool is created using Flask-MySQL.
        Hashing salt is defined as a static variable.

#   User Model:

        A simple User class is defined to represent a user with an ID and user type.
#   User Loader Function:

        This function retrieves user information from the database based on the provided user ID.
        It uses the getUserRole function to get the user type.

#   Helper Functions:

    1.generate_salt: 
        Returns a static salt value for password hashing.
    2.generate_menu: 
        This function dynamically generates the menu list based on the user type. It checks the current user's user type and returns a list of dictionaries containing menu item names and links.
#   API Routes:
1.  Default Route
        1.  /: Renders the index template.
        2.  /login: Renders the login template.
        3.  /signup: Renders the signup template (likely for agronomists).
        4.  /agronosmist_signup: Handles agronomist signup form submission, creates a new user with hashed password in the database and redirects to the login page.
        5.  /update_profile: Handles GET and POST requests for updating user profile. On GET, it retrieves the user's information and renders the update profile template. On POST, it updates the user's details in the database and redirects to the profile page with a success message.
        6.  /check_user: Handles login form submission, checks username and password against the database (with hashed password comparison), and logs the user in with Flask-Login if credentials are valid. Otherwise, redirects to the login page with an error message.
        7.  /logout: Logs out the user with Flask-Login and redirects to the login page.
        8.  /dashboard: Renders the dashboard template and includes the generated menu list.
2.  Pest and Weed Details:

        1.  /pest_list/<id>: Retrieves details of a specific pest (agriculture item) based on the provided ID. It also fetches associated images from the database and renders the pest details template.
        2. /pest-details: Retrieves a list of active primary pests from the database and renders the pest details template.
        3.  /weed_list/<id>: Similar to /pest_list, retrieves details of a specific weed.
        4.  /weed_details: Similar to /pest-details, retrieves a list of active primary weeds.

3.  Staff Management:

        1.  /add_item: Handles adding a new agriculture item (pest/weed) along with details, biology, impacts, controls, and information. It also handles uploading multiple images and setting the primary image.
        2   /agronomist_list: Retrieves a list of agronomists (user type 3) from the database and renders the agronomist list template.
        3.  /staff_details: Retrieves a list of staff (user type 2) from the database and renders the staff details template.
        4.  /user_list/<id>: Retrieves details of a specific staff member based on the ID.
        5.  /update_staff: Handles updating staff member details. On GET, retrieves staff information and renders the update staff template. On POST, updates the details in the database and redirects to the staff list with a success message.
        6.  /add_staff: Renders the staff add template.

4.  Other Routes:

        1.  /view_item: Retrieves a list of active primary agriculture items and renders the view item template.
        2.  /delete_item/<int:item_id>: Deletes (soft delete by setting is_active to 0) an agriculture item based on the ID and redirects to the view item page.
        3.  /edit_item/<id>: This route definition ends abruptly without implementation. It likely retrieves details of an agriculture item for editing purposes.