# packages/markitdown/tests/test_files/test_wikipedia.html

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/tests/test_files/test_wikipedia.html",
  "file_hash": "4c1f6c5ca1147455b8df8b19cd957844cad37d23d541c039af421a7634074ea6",
  "last_updated": "2025-12-23T15:57:05.349780+00:00",
  "functions": {
    "org": {
      "hash": "f7fbebf53d403598707453f345411a2d1741e43349b19685b97c2e683bd9e060",
      "lines": "830-830",
      "last_updated": "2025-12-23T15:56:58.359339+00:00"
    },
    "and": {
      "hash": "cdf3ce90a4ec406b5c070968e2e55993e1736300e985cccfddceb67e2b15dccd",
      "lines": "2099-2099",
      "last_updated": "2025-12-23T15:57:05.349680+00:00"
    }
  }
}
```

</details>



The file `test_wikipedia.html` is an HTML document structured to represent a Wikipedia page about Microsoft. It implements standard HTML5 elements including a `head` section containing metadata, links to stylesheets, and scripts, as well as a `body` section that organizes the content into navigational elements, headers, and sections for user interaction. The document uses various classes and IDs to facilitate styling and functionality, specifically tailored for the Wikipedia interface.

The main structural elements include a header with navigation menus, a search box, and links to user tools. Notable classes such as `vector-header`, `vector-main-menu`, and `vector-search-box` are defined to manage the layout and user interaction features. The file does not define any functions or classes in the traditional programming sense, as it is primarily an HTML document. However, it utilizes JavaScript through the inclusion of external scripts, specifically for dynamic features such as the search functionality and menu interactions.

The document relies on external resources, including stylesheets loaded from the MediaWiki ResourceLoader, which are essential for the visual presentation of the page. It also references various metadata properties for Open Graph, which are used for social media integration. The data structures manipulated in this file are primarily HTML elements and attributes, such as `<div>`, `<nav>`, and `<a>`, which are utilized to create a structured and interactive user interface. The file does not define any custom data types or interfaces, as it strictly adheres to HTML standards.

## Functions and Classes

## `org`

**Location:** [`packages/markitdown/tests/test_files/test_wikipedia.html:830`](/packages/markitdown/tests/test_files/test_wikipedia.html#L830)

# Function Documentation: org

## Description
The `org` function generates an HTML representation of an information box (infobox) for a company, specifically Microsoft Corporation. The output includes various details about the company, such as its name, type, industry, founders, headquarters, and products, formatted in a structured table.

## Parameters
The function does not take any parameters.

## Return Value
The function returns a string containing HTML markup that represents the infobox for Microsoft Corporation. The HTML includes:
- Company name
- Company type
- Ticker symbol and trading information
- International Securities Identification Number (ISIN)
- Industry
- Founding date and location
- Founders
- Headquarters location
- Area served
- Key people
- Products
- Brands

## Dependencies
The function does not explicitly call any external modules, APIs, or services. It relies solely on HTML and CSS for formatting the output.

## Usage Example
To use the `org` function, simply invoke it without any parameters:

```html
org();
```

This invocation will produce an HTML structure that can be rendered in a web page to display the information about Microsoft Corporation.

---
## `and`

**Location:** [`packages/markitdown/tests/test_files/test_wikipedia.html:2099`](/packages/markitdown/tests/test_files/test_wikipedia.html#L2099)

# Function Documentation: and

## Description
The provided code does not implement a function named `and`. Instead, it contains HTML and CSS code for rendering a navigation bar and related elements on a webpage. The code includes styles for various classes and structures for displaying portal links and sister project links related to Microsoft.

## Parameters
The code does not define any parameters as it does not contain a function implementation. It consists solely of HTML and CSS for layout and styling purposes.

## Return Value
The code does not return a value, as it does not contain a function. It generates HTML content that is rendered in a web browser.

## Dependencies
The code does not explicitly call any external modules, APIs, or services. It relies on standard HTML and CSS for rendering the content.

## Usage Example
Since the code does not define a function, there is no invocation pattern. However, the HTML structure can be included in a webpage to display the navigation bar and sister project links related to Microsoft.

### Example HTML Usage
To use the provided code in a webpage, include it within the body of the HTML document:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Example Page</title>
</head>
<body>
    <!-- Insert the provided HTML code here -->
    <div class="portal-bar noprint metadata noviewer portal-bar-bordered" role="navigation" aria-label="Portals">
        <span class="portal-bar-header"><a href="/wiki/Wikipedia:Contents/Portals" title="Wikipedia:Contents/Portals">Portals</a>:</span>
        <ul class="portal-bar-content">
            <li class="portal-bar-item"><span typeof="mw:File"><span><img alt="" src="//upload.wikimedia.org/wikipedia/commons/thumb/2/2a/Industry5.svg/19px-Industry5.svg.png" decoding="async" width="19" height="19" class="mw-file-element" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/2/2a/Industry5.svg/29px-Industry5.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/2/2a/Industry5.svg/38px-Industry5.svg.png 2x" data-file-width="512" data-file-height="512" /></span></span>&#160;<a href="/wiki/Portal:Companies" title="Portal:Companies">Companies</a></li>
            <li class="portal-bar-item"><span class="mw-image-border" typeof="mw:File"><span><img alt="flag" src="//upload.wikimedia.org/wikipedia/en/thumb/a/a4/Flag_of_the_United_States.svg/21px-Flag_of_the_United_States.svg.png" decoding="async" width="21" height="11" class="mw-file-element" srcset="//upload.wikimedia.org/wikipedia/en/thumb/a/a4/Flag_of_the_United_States.svg/32px-Flag_of_the_United_States.svg.png 1.5x, //upload.wikimedia.org/wikipedia/en/thumb/a/a4/Flag_of_the_United_States.svg/42px-Flag_of_the_United_States.svg.png 2x" data-file-width="1235" data-file-height="650" /></span></span>&#160;<a href="/wiki/Portal:United_States" title="Portal:United States">United States</a></li>
        </ul>
    </div>
    <!-- Additional content can be added here -->
</body>
</html>
``` 

This example demonstrates how to incorporate the provided code into a standard HTML document for rendering a navigation interface.

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
