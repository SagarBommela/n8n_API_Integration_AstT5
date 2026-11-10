
# N8N API Integration – Topic 5: Building API Workflows

## 1. Project Overview

**Project Name:** N8N API Chaining Workflow

**Course:** N8N Hands-On API Integration

**Topic:** Topic 5 – Building API Workflows in n8n

**Platform:** n8n

## 2. Objective

The objective of this project is to understand how to build sequential API workflows in n8n.

This project demonstrates:

- Connecting multiple nodes in sequence.
- Passing data between nodes.
- Sending dynamic HTTP headers.
- Generating ISO-8601 timestamps.
- Accessing data from previous nodes.
- Formatting dates using Luxon.
- Using workflow and execution variables.

## 3. Workflow Structure

The workflow contains five nodes.

### 1. Manual Trigger
Starts the workflow manually.

### 2. Set Base User
Creates static user information.

Username: Alice

Department: Engineering

### 3. Postman Echo Headers
- Sends a GET request.
- Connects to Postman Echo API.
- Sends the current transaction timestamp.
- Sends the user's department as an HTTP header.

API:
https://postman-echo.com/headers

### 4. Create Log Entry
- Sends a POST request to JSONPlaceholder.
- Retrieves username from Set Base User.
- Retrieves User-Agent from Postman Echo Headers.
- Generates a timestamp one hour earlier using Luxon.

API:
https://jsonplaceholder.typicode.com/posts

### 5. Output Metadata
Captures the following information:

- Execution ID
- Workflow ID
- Final log title

## 4. Expressions Used

### Current ISO Timestamp

```javascript
{{ $now.toISOString() }}
```

### Department

```javascript
{{ $json.department }}
```

### Ancestor Node Username

```javascript
{{ $('Set Base User').item.json.username }}
```

### User-Agent Header

```javascript
{{ $json.headers['user-agent'] }}
```

### Timestamp One Hour Earlier

```javascript
{{ $now.minus({ hours: 1 }).toFormat('yyyy-MM-dd HH:mm:ss') }}
```

### Execution ID

```javascript
{{ $execution.id }}
```

### Workflow ID

```javascript
{{ $workflow.id }}
```

### Final Log Title

```javascript
{{ $json.title }}
```

## 5. API Request Details

### GET Request

**API:** Postman Echo Headers

**URL:**
https://postman-echo.com/headers

Custom headers:

- X-Transaction-Time
- X-User-Dept

### POST Request

**API:** JSONPlaceholder

**URL:**
https://jsonplaceholder.typicode.com/posts

Request Body:

```json
{
  "title": "Log entry for Alice",
  "body": "User-Agent utilized was PostmanRuntime/7.0",
  "timestamp": "2026-11-10 14:00:00"
}
```

## 6. Tools Used

- n8n
- HTTP Request Node
- Edit Fields (Set) Node
- Postman
- Postman Echo API
- JSONPlaceholder API
- Luxon Date and Time Library

## 7. Conclusion

Successfully implemented the API Chaining Workflow in n8n.

Learned how to connect multiple nodes, pass dynamic data, generate timestamps, access ancestor node values, and capture workflow execution metadata.

This project demonstrates how multiple APIs and workflow nodes can work together in an automated process.


GIT URL:
https://github.com/SagarBommela/n8n_API_Integration_AstT5

Loom Video:

https://www.loom.com/share/60860f4b5e5d44a59687bed3b96d2fbd
