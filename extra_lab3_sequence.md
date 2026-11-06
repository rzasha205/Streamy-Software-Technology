```mermaid
---
title: User Sign Up Flow
---
sequenceDiagram
    autonumber
    actor Browser
    participant SignUpService as Sign Up Service
    participant UserService as User Service
    participant Kafka
    
    links UserService: {"Repository": "[https://example.com/user-service](https://example.com/user-service)"}
    
    Browser->>+SignUpService: GET /sign_up
    SignUpService-->>-Browser: 200 OK (HTML page)
    Browser->>+SignUpService: POST /sign_up
    SignUpService->>SignUpService: Validate input
    
    alt invalid input
        SignUpService-->>Browser: Error
    else valid input
        SignUpService->>+UserService: POST /users
        UserService--) Kafka: User Created Event Published
        Note left of Kafka: other services take action based on this event
        UserService-->>-SignUpService: 201 Created (User)
        SignUpService-->>-Browser: 301 Redirect (Login page)
    end