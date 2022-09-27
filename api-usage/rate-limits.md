# Rate Limits

### **KakaClo API rate limits**

To ensure our platform remains stable and fair for everyone, all KakaClo APIs are rate-limited. We use a variety of strategies to enforce rate limits. We ask developers to use industry standard techniques for limiting calls, caching results, and re-trying requests responsibly.

***

### **Compare rate limits by API**

| API              | Rate-limiting method | Standard limit    |
| ---------------- | -------------------- | ----------------- |
| Admin API (REST) | Request-based limit  | 2 requests/second |

***

### **The leaky bucket algorithm**

All Shoplazza APIs use a leaky bucket algorithm to manage requests. This algorithm lets your app make an unlimited amount of requests in infrequent bursts over time.\
The main points to understand about the leaky bucket metaphor are as follows:

* Each app has access to a bucket. It can hold, say, 120 “marbles”.
* Each second, a marble is removed from the bucket (if there are any). That way there’s always more room.
* Each API request requires you to toss a marble in the bucket.
* If the bucket gets full, you get an error and have to wait for room to become available in the bucket.

***

### **Rate limiting methods**

**Request-based limits**\
Apps can make a maximum number of requests per minute. For example: 120 API requests within 60 seconds. Each request counts equally, regardless of how much or how little data is returned.

This method is used by the REST Admin API.

***

### **REST Admin API rate limits**

REST Admin API rate limits are based on the combination of the app and store. This means that calls from one app don't affect the rate limits of another app, even on the same store. Similarly, calls to one store don't affect the rate limits of another store, even from the same app.

Limits are calculated using the leaky bucket algorithm. All requests that are made after rate limits have been exceeded are throttled and an HTTP 429 Too Many Requests error is returned. Requests succeed again after enough requests have emptied out of the bucket.

The bucket size and leak rate properties determine the API’s burst behavior and request rate.

The default settings are as follows:

* Bucket size: 120 requests
* Leak rate: 2/second
