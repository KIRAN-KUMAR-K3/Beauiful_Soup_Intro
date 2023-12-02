
---

# Beautiful Soup Introduction

## Table of Contents
- [Introduction](#introduction)
- [Beautiful Soup](#beautiful-soup)
- [Basic Terms in Web Scraping](#basic-terms-in-web-scraping)
- [Types of Parser](#types-of-parser)
- [Making a Soup from HTML File](#making-a-soup-from-html-file)
- [Making a Soup from Any Website HTML](#making-a-soup-from-any-website-html)
- [Analysis of HTML Tags](#analysis-of-html-tags)
- [Navigable Strings](#navigable-strings)
- [Navigating Through Tag Names](#navigating-through-tag-names)
- [Navigating Through Child Tags](#navigating-through-child-tags)
- [Navigating Down the HTML Parse Tree](#navigating-down-the-html-parse-tree)
- [Navigating Up the HTML Parse Tree](#navigating-up-the-html-parse-tree)
- [Navigating Sideways Through Siblings](#navigating-sideways-through-siblings)

---

## Introduction

The essential fundamentals of web scraping involve understanding the basics of HTML and CSS. HTML provides the structure for a web page, and CSS beautifies the webpage. To perform web scraping, you need to explore the web page structure using developer tools, make HTTP requests, and parse the HTML responses to extract specific structured information using tools like Beautiful Soup.

---

## Beautiful Soup

Beautiful Soup is a Python library designed for extracting data from HTML, XML, and other markup languages. It assists in pulling specific content from a webpage, removing HTML markup, and saving the information. This process is suitable for static content available by making an HTTP request to get the webpage content.

---

## Basic Terms in Web Scraping

1. **Crawler**: A web bot that visits web pages and accumulates links (URLs) of nodes, deriving new URLs from each new web page it visits. It does not go deep unless programmed explicitly.

2. **Scraper**: A bot that visits web pages of a given set of URLs, retrieving relevant data to store into a data storage. It does not collect new URLs like a crawler.

3. **Parser**: An offline robot that processes or analyzes given data to derive proper data structures. It retrieves information from unstructured data, whether from data storage or directly from the web (e.g., HTML).

---

## Types of Parser

1. **html.parser**: Built-in, no extra dependencies needed.
2. **html5lib**: The most lenient, better to use if HTML is broken.
3. **lxml**: The fastest.

---

## Making a Soup from HTML File

To create a soup (parse the HTML tree) using Beautiful Soup:

```python
from bs4 import BeautifulSoup

def read_file():
    file = open('intro_to_soup_html.html')
    data = file.read()
    file.close()
    return data

html_file = read_file()
soup = BeautifulSoup(html_file, 'lxml')
```

---

## Making a Soup from Any Website HTML

Install the required library:

```python
pip install fake_useragent
```

Use Beautiful Soup to parse HTML from a website:

```python
import requests
from bs4 import BeautifulSoup
from fake_useragent import UserAgent

ua = UserAgent()
header = {'user-agent': ua.chrome}
google_page = requests.get('https://www.google.com', headers=header)
soup = BeautifulSoup(google_page.content, 'lxml')
print(soup.prettify())
```

---

## Analysis of HTML Tags

Accessing and modifying HTML tags:

```python
meta = soup.meta
div = soup.div

# Accessing attributes
print(meta.get("charset"))
print(meta["charset"])

# Modify attributes at runtime
body = soup.body
body['style'] = 'some style'
```

---

## Navigable Strings

Accessing and modifying navigable strings:

```python
title = soup.title

# Accessing string inside a tag
print(title.string)

# Replace navigable string
title.string.replace_with("title has been changed")
```

---

## Navigating Through Tag Names

Accessing tags directly from their tag names:

```python
title = soup.title
p = soup.p
print(title)
print(p)
```

---

## Navigating Through Child Tags

Navigating through child tags using `.contents` and `.children`:

```python
head = soup.head
body = soup.body

# Using .contents
print(head.contents)
print(body.contents)

# Using .children
for child in body.children:
    print(child if child is not None else '')
```

---

## Navigating Down the HTML Parse Tree

Moving down the HTML parse tree using `.parent`:

```python
title = soup.title
parent = title.parent
print(parent)
print(parent.name)
```

---

## Navigating Up the HTML Parse Tree

Moving up the HTML parse tree using `.parent`:

```python
title = soup.title
p = soup.p
html = soup.html
print(title.parent.name)
print(html.parent)  # returns None as it is at the top of the hierarchy
```

---

## Navigating Sideways Through Siblings

Moving sideways through siblings using `.next_sibling` and `.previous_sibling`:

```python
p = soup.body.p

# Moving sideways
print(p.next_sibling.next_sibling)

# Moving upwards
print(body.previous_sibling.previous_sibling)
```

Feel free to explore these examples and enhance your understanding of Beautiful Soup for web scraping. Happy coding!
