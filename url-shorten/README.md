# Url Shortening Service
URL-shortener is used to create shorter aliases for long urls.THese alises are called **short links**.<br/>
Users are redirected to original url when they hit these short links. <br/>

Short links save a lot of space when displayed, printed,
messaged, or tweeted.


## STEP-1: requirements specification
functional requirements
1. Given a url , our service should generate a shoreter and unique alias of the url.
2. when users access a short link , our service should redirect them to the original link
3. users should optionally be able to pick a custom short link for thier URL
4. Links will expire after a standard default timespan.

non-functional requirements
1. the system should be highly available(uptime)
2. URL redeirection should happen in real-time with minimal latency
3. shortened links should not be guessable

extended requirements
1. analytics eg, how many times a redirection happened
2. our service should also be accessible through REST APIS by other services
## STEP-2:System interface definition

it will be REST api with following endpoints
    - create-url `create new short link`
    - login `login a user account`
    - register  `create a user account`


## STEP-3: back-of-the-envlope estimations.
Since there will be alots of redirection requests compared to new url shortenings.

Traffic estimates:
    new URLS shortenings per second = 200 URLs/s
    urls redirections per second = 20,000 URLs/s

storage estimates:
    1GB hard-disk space to store data

bandwidth estimates:
    10 MB/s
memory estimates
    IGB space

## STEP-4: defing data model
since there is no need for `relationships` between objects - a `NoSQL` database will work.

database schema
    USERS:
        email
        created-at
        lastLogin
        name
        total_links
    URL
        original_url
        creation_date
        expiration_date
        userID
        alias

## STEP-5:High level design
objectives - generate a short and unique key for a given url

components
1. load blanacer
2. Application servers( for read/write)
3. Url Key Generator (oonline or offline)
4. Database (MongoDB)
5. Cache (redis for faster redirection)
6. Analytics worker( kafka and clickchouse)


## STEP-6: Detailed Design
(a).encoding actual url

(b)caching

(c) redirection flow
- GET `/abc123`
- check redis cache
- if not found query DB
- redeirect with `302 Found`


## STEP-7: Bottlenecks & Scaling
Read-heavy: Use Redis to cache redirects

Writes: Use a background job to store usage analytics

DB: Shard based on short_code or user

Collision risk: Use proper key space + uniqueness check


## STEP-8: summary
Redis improves performance

Scales well with sharding and stateless services

Flexible to support features like expiry, analytics