


#### Using Apollo Client for server side rendered page data

Fetching data for server-side generated pages is done using the `getServerSideProps` method provided by Next.js. This function will be used during each page request to get any data passed into the page component as props.

![](https://wp.apollographql.com/wp-content/uploads/2021/03/Server-side_Rendering_3-1024x410.png)



Apollo Caching 

**cache-first:**

The default fetch policy for Apollo is cache-first. If you do not set a fetch policy yourself, this is what will be used. It favors quick response times for queries over getting the most up-to-date data. If you don’t expect your data to change, or if you are taking care to explicitly update the cache when changes are made, this is a good option. With a cache first fetch-policy:

1.  You query for some data. Apollo checks the cache for the data. _If all of the data is present in the cache, skip directly to step 4._
2.  If the cache is missing some of the data you asked for, Apollo will make a network request to your API.
3.  The API responds with the data, Apollo uses it to update the cache.
4.  The requested data is returned.

**cache-and-network:**

I have found ‘cache-and-network’ to be a good option for displaying data that gets updated frequently. While the ‘cache first’ policy emphasizes quick responses to queries, ‘cache-and-network’ puts a little more weight on keeping the cache up-to-date with what is on the server. Implementing this fetch policy can be a good fix if you have data that is changing frequently and your queries are returning out-of-date information.

1.  You query for some data. Apollo checks the cache for the data.
2.  If the data is in the cache, return that cached data.
3.  Regardless of whether any data was found in step two, pass the query along to the API to get the most up-to-date data.
4.  Update the cache with any new data from the API.
5.  Return the updated API data.

**network-only:**

If you do not want to risk displaying any out-of-date information from the cache, it may make sense to use a ‘network-only’ fetch policy. This policy favors showing the most up-to-date information over quick responses. Unlike ‘cache-and-network’, this policy will never return possibly outdated information from the cache. It will also keep your cache up-to-date for future queries.

1.  Apollo makes a network request for your data without checking the cache.
2.  The server responds with your data and the cache is updated.
3.  The data is returned.

**no-cache:**

The ‘no-cache’ policy is similar to ‘network-only’, but it skips the step of updating the cache. This might be appropriate if you don’t want to store certain information in your cache at all.

1.  Apollo makes a network request for your data without checking the cache.
2.  The server responds and the data is returned without updating the cache.

**cache-only:**

The opposite of no-cache, this fetch policy avoids making any network requests. If the data you are querying is not available in the cache, it will throw an error. This can be useful if you want to display consistent information to the user, ignoring any server-side changes. It may also be useful if you want to enable parts of your application to work offline.

1.  Apollo checks the cache for queried data.
	1.  If all the data is present in the cache, it is returned (otherwise, an error is thrown).