# Backend and Frontend Integration Description

## API Client Architecture

A generic, type-safe HTTP client for REST API calls:

### Features:

* TypeScript generic support for type-safe responses
* JWT authentication via headers
* JSON/text response handling
* Optional request/response logging
* Relay mode for external APIs
* No-cache policy for fresh data

### Parameters:

* endpoint - API endpoint path
* method - HTTP method (GET, POST, PUT, DELETE)
* headers - Custom headers (e.g., Authorization)
* body - Request payload (auto-serialized)
* isJson - Response type toggle (default: true)
* log - Debug logging toggle
* relay - External API mode (bypasses base URL)

## Data Fetching Patterns

### Technology Stack:

* React Query - Data fetching and caching
* Zustand - Client-side state management
* Custom WebSocket Hook - Real-time data streaming

#### API Client and Data Fetching Testing

We tested all backend integrated APIs using the fetch/XHR tab under the network tab of `Developer Tools`  tab in google chrome

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>



## WebSocket Integration

### Features:

* Automatic reconnection with exponential backoff
* Ping/pong heartbeat mechanism
* JWT authentication support
* Multi-message handling
* Clean connection lifecycle management

#### Websocket Testing

We tested all backend integrated websocket using the socket tab under the network tab of `Developer Tools`  tab in google chrome

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

## Testing Coverage

### Test Scenarios:

* GET/POST/PUT requests with bodies
* Custom header merging (Authorization)
* JSON/text response handling
* Error handling (404, 500, network errors)
* Relay mode (external APIs)
* Request/response logging
* Null/undefined body handling
* Environment variable handling











