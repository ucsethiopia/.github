## Hi there 👋

- Ultimate Consultancy Services is a consulting firm making a positive difference in organizations' and individuals' lives through the provision of advisory, consultancy, research, and training services.

## Platform Architecture

UCS Ethiopia is supported by a public consulting website and several focused backend services.
All APIs Service Uptime Status Report: https://ultimate-consultancy-services.betteruptime.com/

```mermaid
flowchart TD
    Visitor[Website visitor] --> Website[ucs-ui<br/>Public Next.js website]

    Website -->|Contact form| UCS[ucs-service]
    Website -->|Team profiles| UCS
    Website -->|Published news| SocialPublic[social-stream public API]
    Website -->|Economic dashboard| MarketData[market-data API]

    UCS --> UCSPostgres[(PostgreSQL)]
    UCS --> TeamFiles[(Team JSON files)]
    UCS --> Mail[Mailgun or SMTP]

    Admin[Company admin or editor] --> Clerk[Clerk]
    Admin --> SocialInternal[social-stream internal API]
    Clerk --> SocialInternal

    SocialInternal --> SocialPostgres[(PostgreSQL)]
    SocialInternal --> B2[Backblaze B2]
    SocialInternal --> Platforms[Instagram, Facebook,<br/>LinkedIn, Telegram]
    SocialInternal --> Audit[Audit logs]

    MarketData --> Redis[(Redis current values)]
    MarketData --> Mongo[(MongoDB historical series)]
    MarketData --> Sources[External market APIs<br/>and scheduled scrapers]

