# API Documentation

## API Overview

The REST API for Local Deep Research provides a suite of tools for in-depth analysis and information retrieval. It allows users to generate quick summaries, create comprehensive research reports, and analyze documents. The API is designed to be easy to integrate and provides clear, structured responses.

## Version

The current version of the API is **v1**.

## Available Endpoints

The following are the main endpoints available in the API:

-   **POST /api/v1/quick_summary**
    -   **Description:** Generates a quick summary for a given topic.
    -   **Parameters:** `topic` (string), `max_length` (integer)

-   **POST /api/v1/generate_report**
    -   **Description:** Generates a comprehensive research report on a given topic.
    -   **Parameters:** `topic` (string), `report_format` (string, e.g., "pdf", "docx")

-   **POST /api/v1/analyze_documents**
    -   **Description:** Analyzes a list of documents and extracts key information.
    -   **Parameters:** `documents` (array of strings), `analysis_type` (string, e.g., "sentiment", "keywords")

## Request and Response Format

### Request

Requests to the API should be made with a `Content-Type` of `application/json`. The request body should be a JSON object containing the required parameters for the endpoint.

**Example Request to `/api/v1/quick_summary`:**

```json
{
    "topic": "The future of AI",
    "max_length": 200
}
```

### Response

The API returns a JSON object for all responses.

**Success Response:**

A successful request will return a `200 OK` status code and a response body with the following structure:

```json
{
    "code": 0,
    "message": "success",
    "data": {
        "summary": "This is a summary of the future of AI..."
    }
}
```

**Error Response:**

An error will return a non-200 status code and a response body with the following structure:

```json
{
    "code": 1001,
    "message": "Invalid topic provided",
    "data": null
}
```

## Authentication

The API uses an API key for authentication. You must include your API key in the `x-api-key` header of every request.

**Example Header:**

```
x-api-key: YOUR_API_KEY
```

Requests without a valid API key will result in an authentication error.

## Error Handling

The API uses the following error codes:

-   `1001`: Invalid input - The request parameters are invalid.
-   `1002`: Authentication error - The API key is missing or invalid.
-   `1003`: Not found - The requested resource could not be found.
-   `2001`: Internal server error - An unexpected error occurred on the server.

Your application should handle these errors gracefully.

## Usage Limits and Best Practices

-   **Rate Limits:** The API has a rate limit of 100 requests per minute.
-   **Best Practices:**
    -   Cache responses when possible to avoid unnecessary API calls.
    -   Use a backoff strategy when you receive a rate limit error.
    -   Keep your API key secure and do not expose it in client-side code.
