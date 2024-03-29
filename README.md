# Safelock License System - API Documentation

Welcome to the Safelock License System - API Documentation. This API provides endpoints for managing licenses within your system. It allows users to perform operations such as fetching, creating, deleting licenses, products and much more.

## API Routes
- **Developer:** - https://base.url/api/dev
- **Client:** - https://base.url/client/dev
- **User:** - https://base.url/users/dev


## User Route

### Login
- **URL**: `/login`
- **Method**: POST
- **Description**: Authenticates a user and generates a refresh token.
- **Request Body**:
  - `email` (string): User's email or username.
  - `password` (string): User's password.
  - `twofactor` (string): Two-factor authentication code (optional).
- **Response**:
  - `msg` (string): Message indicating the result of the operation.

### Logout
- **URL**: `/logout`
- **Method**: GET
- **Description**: Logs out the user by clearing the refresh token cookie.
- **Response**:
- `msg` (string): Message indicating the result of the operation.

### Refresh Token
- **URL**: `/refresh_token`
- **Method**: POST
- **Description**: Generates a new access token using the refresh token stored in the cookies.
- **Authorization**: Requires the presence of the refresh token in the cookies.
- **Response**:
  - `access_token` (string): New access token.

### Get User Information
- **URL**: `/infor`
- **Method**: GET
- **Description**: Retrieves user information.
- **Authorization**: Required
- **Response**:
  - User object without password and licenses fields.


### Get Blacklist Data
- **URL**: `/getblacklist`
- **Method**: GET
- **Description**: Retrieves blacklisted data with pagination.
- **Authorization**: Required
- **Query Parameters**:
  - `page` (number, optional): Page number for pagination.
  - `limit` (number, optional): Limit of items per page.
- **Response**:
  - `total` (number): Total count of blacklisted items.
  - `blacklist` (object): Object containing paginated blacklisted data.
    - `results` (array): Array of blacklisted items within the requested page.
    - `next` (object, optional): Object containing page number and limit for the next page.
    - `prev` (object, optional): Object containing page number and limit for the previous page.

### Add Blacklist Data
- **URL**: `/addblacklist`
- **Method**: POST
- **Description**: Adds a new entry to the blacklist.
- **Authorization**: Required
- **Request Body**:
  - `blacklisted` (string, required): IP address or HWID to be blacklisted.
  - `type` (string, required): Type of entry, either "ip" or "hwid".
  - `product` (string, required): Product associated with the blacklisted entry.
  - `created_by` (string, required): ID of the user who created the blacklist entry.
- **Response**:
  - `msg` (string): Message indicating the result of the operation.

### Delete Blacklist
- **URL**: `/deleteblacklist`
- **Method**: POST
- **Description**: Deletes a blacklisted entry.
- **Authorization**: Required
- **Request Body**:
  - `blacklisted` (string, required): ID of the blacklisted entry to be deleted.
- **Response**:
  - `msg` (string): Message indicating the result of the operation.

### Create User
- **URL**: `/createuser`
- **Method**: POST
- **Description**: Creates a new user.
- **Authorization**: Required
- **Request Body**:
  - `created_by` (string, required): ID of the user who is creating the new user.
  - `data` (object, required): Object containing user details.
    - `name` (string, required): Name of the user.
    - `email` (string, required): Email of the user.
    - `password1` (string, required): Password of the user.
    - `password2` (string, required): Confirmation password of the user.
    - `permission` (number, required): Permission level of the user.
- **Response**:
  - `msg` (string): Message indicating the result of the operation.

### Delete User
- **URL**: `/deleteuser`
- **Method**: POST
- **Description**: Deletes a user.
- **Authorization**: Required
- **Request Body**:
  - `user` (object, required): Object containing the email of the user to be deleted.
- **Response**:
  - `msg` (string): Message indicating the result of the operation.

### Get Users
- **URL**: `/getusers`
- **Method**: GET
- **Description**: Retrieves all users.
- **Authorization**: Required
- **Response**:
  - `users` (array): Array of user objects excluding sensitive information.

### Update User
- **URL**: `/updateuser`
- **Method**: POST
- **Description**: Updates a user.
- **Authorization**: Required
- **Request Body**:
  - `editing` (object, required): Object containing updated user details.
    - `_id` (string, required): ID of the user to be updated.
    - `name` (string): Updated name of the user.
    - `email` (string): Updated email of the user.
    - `role` (number): Updated permission level of the user.
- **Response**:
  - `msg` (string): Message indicating the result of the operation.

### Create Product
- **URL**: `/createproduct`
- **Method**: POST
- **Description**: Creates a new product.
- **Authorization**: Required
- **Request Body**:
  - `data` (object, required): Object containing product details.
    - `price` (number, required): Price of the product.
    - `role` (number, required): Role associated with the product.
    - `version` (string, required): Version of the product.
    - `download` (string, required): Download link of the product.
    - `name` (string, required): Name of the product.
- **Response**:
  - `msg` (string): Message indicating the result of the operation.

### Get Products
- **URL**: `/getproducts`
- **Method**: GET
- **Description**: Retrieves all products.
- **Authorization**: Required
- **Response**:
  - `products` (array): Array of products.
  - `latest` (string): Name of the latest product.

### Delete Product
- **URL**: `/deleteproduct`
- **Method**: POST
- **Description**: Deletes a product.
- **Authorization**: Required
- **Request Body**:
  - `product` (string, required): ID of the product to be deleted.
- **Response**:
  - `msg` (string): Message indicating the result of the operation.

### Update Product
- **URL**: `/updateproduct`
- **Method**: POST
- **Description**: Updates a product.
- **Authorization**: Required
- **Request Body**:
  - `editing` (object, required): Object containing updated product details.
    - `_id` (string, required): ID of the product to be updated.
    - `name` (string, required): Updated name of the product.
    - `role` (number, required): Updated role associated with the product.
    - `version` (string, required): Updated version of the product.
    - `discount` (number, required): Updated discount percentage of the product.
    - `price` (number, required): Updated price of the product.
- **Response**:
  - `msg` (string): Message indicating the result of the operation.


## Client Route

### Verify License
- **URL**: `/`
- **Method**: POST
- **Description**: Verifies a license key for a product.
- **Request Body**:
  - `product` (string, required): Name of the product associated with the license.
  - `licensekey` (string, required): License key to verify.
  - `hwid` (string, optional): Hardware ID associated with the client.
  - `version` (string, optional): Version of the product.
- **Response**:
  - `status_msg` (string): Message indicating the status of the authentication.
  - `status_overview` (string): Overview of the authentication status (success/failed).
  - `status_code` (number): HTTP status code of the response.
  - `status_id` (string): Unique status ID generated based on the request and license key.
  - `description` (string): Description of the license.
  - `version` (string): Version of the product.
  - `clientname` (string): Name of the client associated with the license.
  - `discord_username` (string): Discord username of the client (if available).
  - `discord_id` (string): Discord ID of the client (if available).
  - `expires` (string): Expiry information of the license.


## Developer Route

### Get Licenses
- **URL**: `/licenses/get`
- **Method**: GET
- **Description**: Fetches licenses from the database based on optional query parameters.
- **Query Parameters**:
  - `license` (string, optional): Filter licenses by license key.
  - `clientname` (string, optional): Filter licenses by client name.
  - `product` (string, optional): Filter licenses by product name.
- **Response**:
  - `msg` (string): Success message.
  - `total` (integer): Total number of licenses fetched.
  - `licenses` (array): Array of license objects.

### Create License
- **URL**: `/licenses/create`
- **Method**: POST
- **Description**: Creates a new license and adds it to the database.
- **Request Body**:
  - `product` (string, required): Name of the product associated with the license.
  - `clientname` (string, required): Name of the client.
  - `discord_id` (string, optional): Discord ID of the client.
  - `description` (string, optional): Description of the license.
  - `expires` (boolean, required): Indicates whether the license expires.
  - `expires_delete_after` (boolean, optional): Indicates whether to delete the license after expiry.
  - `expires_type` (string, optional): Type of expiry (e.g., 'days', 'date', 'times').
  - `expires_days` (number, optional): Number of days until expiry.
  - `expires_date` (string, optional): Expiry date in the format 'MM/DD/YYYY'.
  - `expires_times` (number, optional): Number of times the license expires.
  - `expires_start_on_first` (boolean, optional): Indicates whether expiry starts on the first use.
  - `ip_cap` (number, optional): Maximum number of IP addresses allowed.
  - `ip_expires` (number, optional): Expiry duration for IP addresses.
  - `hwid_cap` (number, optional): Maximum number of hardware IDs allowed.
  - `prefer_discord` (boolean, optional): Indicates preference for Discord.
  - `hwid_expires` (number, optional): Expiry duration for hardware IDs.
  - `receive_webhooks` (boolean, optional): Indicates whether to receive webhooks.
  - `pre_ips_list` (array of strings, optional): List of pre-approved IP addresses.
  - `tags` (object, optional): Tags associated with the license.
  - `active` (boolean, optional): Indicates whether the license is active.
  - `created_by` (string, optional): Creator of the license.
- **Response**:
  - `msg` (string): Message indicating the success or failure of the operation.
  - `license` (object): Details of the created license, including the license key.
