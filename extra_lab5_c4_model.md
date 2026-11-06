```mermaid
---
title: "Listing Service C4 Model: Container Diagram"
---
flowchart TD
    User["Premium Member\n[Person]\n\nA user of the website who has\npurchased a subscription"]
    WA["Web Application\n[.NET Core MVC Application]\n\nAllows members to view and review titles\nfrom a web browser. Also exposes\nan API for the mobile app"]
    MA["Mobile Application\n[Xamarin Application]\n\nAllows members to view and review\ntitles from their mobile devices"]
    R[("In-Memory Cache\n[Redis]\n\nTitles and their reviews\nare cached")]
    K["Message Broker\n[Kafka]\n\nImportant domain events\nare published to Kafka"]
    TS["Title Service\n[Software System]\n\nProvides an API to retrieve\ntitle information"]
    RS["Reviews Service\n[Software System]\n\nProvides an API to retrieve\nand submit reviews"]
    SS["Search Service\n[Software System]\n\nProvides an API to search\nfor titles"]
    User-- "Views titles, searches titles\nand reviews titles using\n[HTTPS]" -->WA
    User-- "Views titles, searches titles\nand reviews titles using\n[HTTPS]" -->MA
    subgraph listing-service [Listing Service]
        MA-- "Makes API calls to\n[HTTPS]" -->WA
        WA-- "Reads and writes to\n[REdis Serialization Protocol]" -->R
    end
    WA-. "Publishes messages to\n[Binary over TCP]" ..->K
    WA-- "Makes API calls to\n[HTTPS]" --->TS
    WA-- "Makes API calls to\n[HTTPS]" --->RS
    WA-- "Makes API calls to\n[HTTPS]" --->SS
    classDef container fill:#1168bd,stroke:#0b4884,color:#ffffff
    classDef person fill:#08427b,stroke:#052e56,color:#ffffff
    classDef supportingSystem fill:#666666,stroke:#0b4884,color:#ffffff
    
    class User person
    class WA,MA,R container
    class TS,RS,SS,K supportingSystem
    
    style listing-service fill:none,stroke:#CCC,stroke-width:2px,stroke-dasharray:5 5