xmlserializer serializes a DOM subtree or DOM document into XML/XHTML.

It understands documents generated by [parse5](https://github.com/inikulin/parse5) and regular browser DOMs (and thus can act as a drop-in replacement for [XMLSerializer](https://developer.mozilla.org/en/docs/XMLSerializer) which for some browsers only serializes true XML documents).

[![Build Status](https://secure.travis-ci.org/cburgmer/xmlserializer.png?branch=master)](http://travis-ci.org/cburgmer/xmlserializer)

Limitations
-----------

See [the wiki](https://github.com/cburgmer/xmlserializer/wiki) for limitations in HTML to XML conversion.

Currently some cases are treated differently to the XMLSerializer implementation of the browsers:

- Invalid characters (ASCII control characters) that are invalid in XML 1.0 are removed on serialization. The browsers silently include those characters and on reparsing those documents throw a parser exception.
- Dashes in comments are escaped to provide valid comments in XHTML. Firefox does not do this.
- The `xmlns` attribute has higher precedence than the type of the DOM object passed to the serializer.
- Small differences in style: no space in self-closing tag, empty value for boolean attributes, quoting of single apostrophes in attribute values.

This behaviour might become optional in the future.

Demo
----

See http://cburgmer.github.io/xmlserializer/

Run tests and build for the browser
-----------------------------------

    $ npm install && npm test

Example
-------

For a browser based example run `./go` and see `example.html`.

The same code for Node.js:

```js
var xmlserializer = require('xmlserializer');
var html2xhtml = function (htmlString) {
    var Parser = require('parse5').Parser,
        parser = new Parser(),
        dom = parser.parse(htmlString);

    return xmlserializer.serializeToString(dom);
};
console.log(html2xhtml('<br>'));
// => <html xmlns="http://www.w3.org/1999/xhtml"><head/><body><br/></body></html>
```
