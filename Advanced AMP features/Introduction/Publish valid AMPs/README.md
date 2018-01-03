# How to publish AMPs ⚡
#### Introduction.
There are a few things you need to watch out for when publishing Accelerated Mobile Pages (AMP).


## Publish valid AMPs


One of the great things about AMP is that the runtime includes a built-in validator. <br />The validator checks if your AMP file contains valid AMP HTML. If your page contains invalid AMP, it will not load correctly and third-party platforms might choose not to show your AMP page.<br /> This makes it a good idea to validate a representative subset of your AMP pages to make sure that all different variants are valid.

```
Run the validator by adding #development=1 to an AMP URL
```

There are also other ways to validate an AMP page such as validator.ampproject.org or the official Node AMP Validator, which makes it easy to integrate AMP validation into your build pipeline.
### User correct metadata


Adding metadata to your AMP files enables third-party sites to better display your AMP pages. <br />For example, the Google Top Stories Carousel with AMP currently supports the Article and Video metadata categories and uses these for rendering article previews
The Structured Data Testing Tool is a great way to test whether the metadata in your AMP files is correct:<br /> make sure the “All data” filter shows “AMP Articles” and everything is green. <br />
Here is an [Example](https://search.google.com/structured-data/testing-tool/u/0/?url=https://ampbyexample.com/#url=https%3A%2F%2Fampbyexample.com%2F)


## Be Discoverable
Third-party integrations, such as the Google Top Stories Carousel with AMP, discover your AMPs via the canonical version of your page.<br /> To make this possible, link from your AMP HTML files to their canonical version (this is usually the desktop version):


```
<link rel="canonical" href=”http://example.ampproject.org/article.html" />
```

…and (important!) link to your AMP files from your canonical version (and any alternate):



```
<link rel="amphtml" href="http://example.ampproject.org/article.amp.html" />
```
Otherwise third-party integrations may not be able to discover your AMPs.


## Give Crawlers access

If you want your AMPs to show up in third-party platforms, make sure to allow their crawlers to access them. <br />This means in particular:

* Don’t exclude crawlers via your robots.txt file:
```
User-agent: *
Disallow: /amp/                            <= don't!
```

* Don’t add a robots noindex meta tag to your AMP HTML files:

```
<meta name="robots" content="noindex" />   <= don't!
```

* Don’t include noindex as X-Robots-Tag HTTP header for your AMP files:

```
$ curl -I [http://www.example.com/amp.html](http://www.example.com/amp.html)

HTTP/1.1 200 OK
Date: Tue, 25 May 2010 21:42:43 GMT
...
X-Robots-Tag: noindex                      <= don't!
...
```

## Test with the Google AMP Cache


The Google AMP Cache stores valid AMP pages and provides consistently fast access to them. The Google Top Stories Carousel with AMP, for example, uses the Google AMP Cache to display articles. The cache stores images and fonts in addition to documents. This makes it important to test that your AMPs work correctly when loaded via the Google AMP Cache.
Loading your AMP pages via the Google AMP Cache is easy. The Google AMP Cache URL is composed based on whether the source URL is available via HTTP or HTTPS:<br /><br />
* HTTP: https://cdn.ampproject.org/c/AMP_URL_WITHOUT_SCHEME<br />
* HTTPS: https://cdn.ampproject.org/c/s/AMP_URL_WITHOUT_SCHEME<br />

where AMP_URL_WITHOUT_SCHEME is the location of your AMP file minus http(s)://.<br /> For example, the AMP Cache URL for https://ampbyexample.com is:<br /><br />
https://cdn.ampproject.org/c/s/ampbyexample.com<br /><br />
When loading your AMP pages via the Google AMP Cache, check via your browser’s developer tools if all external resources can be loaded successfully, including all of the following:

* images
* videos
* amp-analytics endpoints
* amp-pixel endpoints
* custom fonts
* iframes

Important: <br />
A common cause for missing assets are protocol relative URLs. <br />
These are currently not supported by the Google AMP Cache. <br />
Instead link to all assets via HTTPS (if available). <br />
You can learn more about how the Google AMP Cache works [here](https://ampbyexample.com/advanced/using_the_google_amp_cache/).
## License

AMP HTML is licensed under the [Apache License, Version 2.0](LICENSE).
