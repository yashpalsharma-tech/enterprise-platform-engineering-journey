<> Markdown
# AWS Global Infrastructure

## AWS Region
Region: A region is a separate geographic location where AWS has data centers. Example: Singapore, Mumbai, New York, Japan regions.

## Availability Zone
An Availability Zone is one more physically separated data centers located within the same AWS region.

## Edge Location
Amazon place copied of frequently used content close to the users, these location are Edge locations.
It only caches the static content but dynamic contents cannot be cached.
Static content are: Images, videos, PDFs, JavaScripts, CSS, software downloads.
Dynamic contents: user id and password.

Amazon uses CloudFront service for caching static contents at the edge locations.

## High Availability
To Keep the application running continuously.

Protects against component failures.
Minimal or no downtime.
Usually within the same AWS Region.

## Disaster Recovery
Protects against large-scale disasters, such as:

Entire Region outage
Earthquake
Major network failure

This typically involves a secondary Region with replicated data and a well-defined failover strategy.

## CloudFront

This is where AWS introduces one of its smartest services.
Instead of making every user contact Singapore directly.
AWS places copies of frequently accessed content closer to users.
These locations are called Edge Locations.

CloudFront uses AWS Edge Locations to deliver content with lower latency.

## Cache Hit vs Cache Miss
A cache hit and cache miss describe whether requested data is found in a cache (a small, fast storage) or not.

## Interview Questions

## Key Takeaways
