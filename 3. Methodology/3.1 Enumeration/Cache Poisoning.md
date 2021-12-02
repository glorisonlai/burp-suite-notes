# Cache Poisoning
**Means of distribution. Chained with other exploits such as XSS, XXE, Deserialization, etc**
**Usually controlled by CDN, but occassionally companies develop their own caching systems**

## Identifying Unkeyed Inputs
**Looking for reflected inputs from normal requests**
**Param Miner -> Guess Headers is good for automating this**
**Note: Set a unique cache key (Cache buster) to identify cached response as yours. Setting to a proxy is useful**
### Common Unkeyed Headers
- X-Forwarded-Host
- X-Forwarded-For
- Origin
- Common request queries (Language, etc)


