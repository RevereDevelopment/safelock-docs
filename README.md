# License System API Documentation

Welcome to the License System API Documentation. This API provides endpoints for managing licenses within your system. It allows users to perform operations such as fetching, creating, and deleting licenses.

## Developer Route

## Base URL
- https://example.com/api/dev

## Endpoints

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
