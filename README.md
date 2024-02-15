# License System API Documentation

Welcome to the License System API Documentation. This API provides endpoints for managing licenses within your system. It allows users to perform operations such as fetching, creating, and deleting licenses.

## Developer Route

### Base URL
- https://example.com/api/dev

### Endpoints

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
