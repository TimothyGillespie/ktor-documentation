[//]: # (title: Caching headers)

<microformat>
<var name="example_name" value="caching-headers"/>
<include src="lib.xml" include-id="download_example"/>
</microformat>

The [CachingHeaders](https://api.ktor.io/ktor-server/ktor-server-core/ktor-server-core/io.ktor.features/-caching-headers/index.html) plugin (previously known as feature) adds the capability to configure the `Cache-Control` and `Expires` headers used for HTTP caching. You can introduce different [caching strategies](#configure) for specific content types, such as images, CSS and JavaScript files, and so on.

## Install CachingHeaders {id="install_feature"}

<var name="feature_name" value="CachingHeaders"/>
<include src="lib.xml" include-id="install_feature"/>

After installing `CachingHeaders`, you can [configure](#configure) caching settings for various content types.

## Configure caching {id="configure"}
To configure the `CachingHeaders` plugin, you need to define the [options](https://api.ktor.io/ktor-server/ktor-server-core/ktor-server-core/io.ktor.features/-caching-headers/-configuration/options.html) function to provide specified caching options for a given content type. The code snippet from the [caching-headers](https://github.com/ktorio/ktor-documentation/tree/main/codeSnippets/snippets/caching-headers) example shows how to add the `Cache-Control` header with the `max-age` option for CSS:

```kotlin
```
{src="snippets/caching-headers/src/main/kotlin/com/example/Application.kt" lines="14-21"}

The [CachingOptions](https://api.ktor.io/ktor-http/ktor-http/io.ktor.http.content/-caching-options/index.html) object accepts `Cache-Control` and `Expires` header values as parameters:

* The `cacheControl` parameter accepts a [CacheControl](https://api.ktor.io/ktor-http/ktor-http/io.ktor.http/-cache-control/index.html) value. You can use [CacheControl.MaxAge](https://api.ktor.io/ktor-http/ktor-http/io.ktor.http/-cache-control/-max-age/index.html) to specify the `max-age` parameter and related settings, such as visibility, revalidation options, and so on. You can disable caching by using `CacheControl.NoCache`/`CacheControl.NoStore`.
* The `expires` parameter allows you to specify the `Expires` header as a `GMTDate` or `ZonedDateTime` value.



## Customize headers for specific routes {id="route_headers"}

If you need to add caching headers for a specific route only, you can append the desired headers into a response. In this case, you don't need to [install](#install_feature) `CachingHeaders`. The code snippet below shows how to disable caching for the `/profile` route:

```kotlin
get("/profile") {
    call.response.headers.append(HttpHeaders.CacheControl, "no-cache, no-store")
    // ... 
}
```

You can learn more about routing in %product% from [](Routing_in_Ktor.md).
