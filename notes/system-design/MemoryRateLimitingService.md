# Memory Rate Limiting Service System Design Document

## Table of Contents
1. Introduction
2. Requirements
3. System Design
   - Overview
   - Components
   - Data Structures
4. Implementation
   - Interface Definition
   - Service Implementation
   - Usage Example
5. Future Enhancements
6. Conclusion

## 1. Introduction

The Memory Rate Limiting Service is designed to restrict the number of requests a client can make within a specified time frame. This document details the design, implementation, and usage of the Memory Rate Limiting Service in Java.

## 2. Requirements

- Ability to set rate limits for different clients.
- Ability to check if a request from a client is allowed based on the set rate limit.
- Maintain rate limiting logic using in-memory data structures.
- Reset request counts after the defined time period (e.g., one minute).

## 3. System Design

### Overview

The system consists of a service that tracks and enforces rate limits for various clients. It uses in-memory data structures to store rate limits, request counts, and timestamps of the last request. The service ensures that clients do not exceed the allowed number of requests per minute.

### Components

1. **RateLimitService Interface**: Defines methods for setting rate limits and checking if requests are allowed.
2. **MemoryRateLimitService Class**: Implements the RateLimitService interface and maintains the in-memory state of request counts and rate limits.
3. **Main Class**: Demonstrates the usage of the MemoryRateLimitService.

### Data Structures

- **HashMap<String, Integer> requestCounts**: Stores the number of requests made by each client within the current time window.
- **HashMap<String, Long> lastRequestTimes**: Stores the timestamp of the last request made by each client.
- **HashMap<String, Integer> rateLimits**: Stores the rate limit (requests per minute) for each client.

## 4. Implementation

### Interface Definition

```java
public interface RateLimitService {
    void setRateLimit(String clientId, int requestsPerMinute);
    boolean allowRequest(String clientId);
}
```

- **setRateLimit(String clientId, int requestsPerMinute)**: Configures the rate limit for a specified client.
- **allowRequest(String clientId)**: Checks if a request from the specified client is allowed based on the rate limit.

### Service Implementation

```java
import java.util.HashMap;
import java.util.Map;

public class MemoryRateLimitService implements RateLimitService {
    private Map<String, Integer> requestCounts = new HashMap<>();
    private Map<String, Long> lastRequestTimes = new HashMap<>();
    private Map<String, Integer> rateLimits = new HashMap<>();

    @Override
    public void setRateLimit(String clientId, int requestsPerMinute) {
        rateLimits.put(clientId, requestsPerMinute);
    }

    @Override
    public boolean allowRequest(String clientId) {
        long currentTime = System.currentTimeMillis();
        int rateLimit = rateLimits.getOrDefault(clientId, 0);
        int requestCount = requestCounts.getOrDefault(clientId, 0);
        long lastRequestTime = lastRequestTimes.getOrDefault(clientId, 0L);

        if (currentTime - lastRequestTime > 60000) { // Reset count if more than 1 minute has passed
            requestCounts.put(clientId, 0);
            lastRequestTimes.put(clientId, currentTime);
        }

        if (requestCount < rateLimit) {
            requestCounts.put(clientId, requestCount + 1);
            lastRequestTimes.put(clientId, currentTime);
            return true;
        } else {
            return false;
        }
    }
}
```
Let's go through the `MemoryRateLimitService` implementation in detail. This service is designed to limit the number of requests a client can make within a specified time frame, using in-memory data structures to track and enforce these limits.

### Class Definition and Fields

```java
public class MemoryRateLimitService implements RateLimitService {
    private Map<String, Integer> requestCounts = new HashMap<>();
    private Map<String, Long> lastRequestTimes = new HashMap<>();
    private Map<String, Integer> rateLimits = new HashMap<>();
```

- **`requestCounts`**: A `HashMap` that keeps track of the number of requests each client has made within the current time window.
- **`lastRequestTimes`**: A `HashMap` that stores the timestamp of the last request made by each client.
- **`rateLimits`**: A `HashMap` that holds the maximum number of requests allowed per minute for each client.

### `setRateLimit` Method

```java
@Override
public void setRateLimit(String clientId, int requestsPerMinute) {
    rateLimits.put(clientId, requestsPerMinute);
}
```

- **Purpose**: This method sets the rate limit for a specific client. It stores the maximum number of requests a client can make per minute in the `rateLimits` map.
- **Parameters**: 
  - `clientId`: A unique identifier for the client.
  - `requestsPerMinute`: The maximum number of requests the client is allowed to make per minute.

### `allowRequest` Method

```java
@Override
public boolean allowRequest(String clientId) {
    long currentTime = System.currentTimeMillis();
    int rateLimit = rateLimits.getOrDefault(clientId, 0);
    int requestCount = requestCounts.getOrDefault(clientId, 0);
    long lastRequestTime = lastRequestTimes.getOrDefault(clientId, 0L);

    if (currentTime - lastRequestTime > 60000) { // Reset count if more than 1 minute has passed
        requestCounts.put(clientId, 0);
        lastRequestTimes.put(clientId, currentTime);
    }

    if (requestCount < rateLimit) {
        requestCounts.put(clientId, requestCount + 1);
        lastRequestTimes.put(clientId, currentTime);
        return true;
    } else {
        return false;
    }
}
```

- **Purpose**: This method checks if a request from a client is allowed based on the client's rate limit. It returns `true` if the request is allowed and `false` otherwise.
- **Steps**:
  1. **Get Current Time**: The current system time in milliseconds is stored in `currentTime`.
  2. **Fetch Rate Limit**: Retrieve the rate limit for the client from `rateLimits`. If no rate limit is found, default to 0.
  3. **Fetch Request Count**: Retrieve the current request count for the client from `requestCounts`. If no count is found, default to 0.
  4. **Fetch Last Request Time**: Retrieve the timestamp of the last request for the client from `lastRequestTimes`. If no timestamp is found, default to 0.
  5. **Check Time Window**:
     - If more than 60 seconds (one minute) have passed since the last request, reset the request count to 0 and update the last request time to the current time.
  6. **Allow or Deny Request**:
     - If the current request count is less than the rate limit, increment the request count, update the last request time, and return `true` to allow the request.
     - If the request count has reached the rate limit, return `false` to deny the request.

### Detailed Explanation

1. **Current Time Calculation**: `long currentTime = System.currentTimeMillis();`
   - This gets the current time in milliseconds since January 1, 1970 (the Unix epoch).

2. **Fetch Rate Limit**: `int rateLimit = rateLimits.getOrDefault(clientId, 0);`
   - The `getOrDefault` method returns the rate limit for the client if it exists; otherwise, it returns 0.

3. **Fetch Request Count**: `int requestCount = requestCounts.getOrDefault(clientId, 0);`
   - Similarly, this retrieves the number of requests the client has made within the current time window or defaults to 0 if no entry exists.

4. **Fetch Last Request Time**: `long lastRequestTime = lastRequestTimes.getOrDefault(clientId, 0L);`
   - This gets the timestamp of the last request made by the client or defaults to 0 if no entry exists.

5. **Check Time Window**:
   ```java
   if (currentTime - lastRequestTime > 60000) { // Reset count if more than 1 minute has passed
       requestCounts.put(clientId, 0);
       lastRequestTimes.put(clientId, currentTime);
   }
   ```
   - This checks if more than 60,000 milliseconds (1 minute) have passed since the last request. If so, it resets the request count to 0 and updates the last request time to the current time.

6. **Allow or Deny Request**:
   ```java
   if (requestCount < rateLimit) {
       requestCounts.put(clientId, requestCount + 1);
       lastRequestTimes.put(clientId, currentTime);
       return true;
   } else {
       return false;
   }
   ```
   - If the request count is less than the rate limit, it increments the request count, updates the last request time, and returns `true` to allow the request.
   - If the request count has reached the rate limit, it returns `false` to deny the request.

This implementation ensures that each client can only make a limited number of requests within a specified time frame (one minute in this case). The counts and timestamps are reset after each time window, allowing clients to make new requests in the next period.

### Usage Example

```java
public class Main {
    public static void main(String[] args) {
        RateLimitService rateLimitService = new MemoryRateLimitService();

        rateLimitService.setRateLimit("client1", 100); // Set rate limit for client1

        for (int i = 0; i < 150; i++) {
            boolean allowed = rateLimitService.allowRequest("client1");
            System.out.println("Request " + (i + 1) + " allowed: " + allowed);
        }
    }
}
```

## 5. Future Enhancements

- **Concurrency Handling**: Use thread-safe data structures like `ConcurrentHashMap` to handle concurrent requests.
- **Persistence**: Integrate with a database to persist rate limits and request counts across service restarts.
- **Distributed Rate Limiting**: Implement a distributed rate limiting mechanism using external caches like Redis.
- **Configuration Management**: Add support for dynamic configuration changes and loading rate limits from external sources.

## 6. Conclusion

This document outlines the design and implementation of a simple Memory Rate Limiting Service in Java. The service uses in-memory data structures to track and enforce rate limits for different clients. Future enhancements can improve concurrency handling, persistence, and scalability.
