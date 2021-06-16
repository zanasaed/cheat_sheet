# Scrapy
Udemy - Modern Web Scraping with Python using Scrapy Splash Selenium 2020-5

this document it is not a tutorail to learn scarapy it is just a note book of importnet thighs that I think it's useful 
# Using Shell

[Doc](https://docs.scrapy.org/en/latest/topics/shell.html?highlight=shell)

The Scrapy shell is an interactive shell where you can try and debug your scraping code very quickly, without having to run the spider. It’s meant to be used for testing data extraction code, but you can actually use it for testing any kind of code as it is also a regular Python shell.

for start:

`scrapy shell`



**Some importent feature of shell**:
1. The shell is used for testing XPath or CSS
2. shell also works for local files.
3. [Available Shortcuts](https://docs.scrapy.org/en/latest/topics/shell.html?highlight=shell#available-shortcuts)
4.[Avalibale Scrapy objects](https://docs.scrapy.org/en/latest/topics/shell.html?highlight=shell#available-scrapy-objects)

get website in sell :

1. before shell and in shell command : `scrapy shell "url"`
2. `fetch("url")`
3. `r = scrapy.Request(url = 'https//:www.google.com')` and `fetch(r)`

for the raw HTML markup get back : 

`response.body`

how scrapy see website : 

`view(response)`

**Note** : scrapy doesn't work with Java script so the part of website it is use Java script it is not visible in scrapy request response

for test xpath it is working:
`response.xpath('//title/text()').get()`

**Note** : when there are multiple element to get back use `getall()` 
`response.xpath('//text()').getall()`

<br>

**Example** :

```
scrapy shell 
r = scrapy.Request('https://www.google.com")
fetch(r) 
response.body 
view(response)
title = response.xpath('h1')

```


**very important part**

[Invoking the shell from spiders to inspect responses
](https://docs.scrapy.org/en/latest/topics/shell.html?highlight=shell#invoking-the-shell-from-spiders-to-inspect-responses)

Sometimes you want to inspect the responses that are being processed in a certain point of your spider, if only to check that response you expect is getting there.

<br>

This can be achieved by using the scrapy.shell.inspect_response function.

<br>

Here’s an example of how you would call it from your spider:

```
import scrapy


class MySpider(scrapy.Spider):
    name = "myspider"
    start_urls = [
        "http://example.com",
        "http://example.org",
        "http://example.net",
    ]

    def parse(self, response):
        # We want to inspect one specific response.
        if ".org" in response.url:
            from scrapy.shell import inspect_response
            inspect_response(response, self)

        # Rest of parsing code.

```

When you run the spider, you will get something similar to this:

```
2014-01-23 17:48:31-0400 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://example.com> (referer: None)
2014-01-23 17:48:31-0400 [scrapy.core.engine] DEBUG: Crawled (200) <GET http://example.org> (referer: None)
[s] Available Scrapy objects:
[s]   crawler    <scrapy.crawler.Crawler object at 0x1e16b50>
...

>>> response.url
'http://example.org'
```