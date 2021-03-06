# tMongoDBXMLOutput

This is a custom component for Talend Open Studio, Big Data Edition
6.0.1, which lets you construct documents as XML and then write them
to MongoDB as JSON.

While Talend has excellent features to construct complex XML
documents, its JSON support is not quite on par with that. This
component allows you to leverage the XML features and use them to
construct MongoDB JSON documents. In particular, this allows you to
have multiple arrays in the same document, while Talend's MongoDB
components can only deal with a single array. It is also possible to
generate all JSON data types that MongoDB supports.

Installation
============

Create a user component directory and place this directory,
tMongoDBXMLOutput, into it.  Let Talend Open Studio know about the
user component directory by specifying it in Preferences->Talend.  You
will then have the new component tMongoDBXMLOutput available in the
palette, along with the existing MongoDB components.

Usage
=====

The original component tMongoDBOutput does not allow a Document as an
incoming column data type.  This component changes that.  You can now
use a single column of type Document as the input.  The component
automatically converts the XML structure of that document to MongoDB
JSON and writes it to the database.

In order to create meaningful JSON, the XML needs to follow a few
conventions.

* Nested XML elements translate naturally to nested JSON documents.
  The top-level root tag is always ignored.  For example, this XML structure::

  ```XML
    <root>
      <name>James Bond</name>
      <address>
        <city>London</city>
        <country>UK</country>
      </address>
    </root>
  ```
  translates to this JSON:
  ```javascript
    {
       "name" : "James Bond",
       "address" : {
          "city" : "London",
          "country" : "UK"
       }
    }
  ```

* Values are normally translated as JSON strings, but you can choose different MongoDB/BSON data types by attaching an attribute @type to the enclosing element.  Supported types as of now include "int", "boolean", and "date".

  ```XML
  <root>
    <balance type="int">31000</balance>
    <consolidated type="boolean">false</consolidated>
    <last_update type="date">2015-01-14 13:22:00</last_update>
  </root>
  ```
  translates to:
  ```javascript
  {
     "balance" : 31000,
     "consolidated" : false,
     "last_update" : ISODate("2015-01-14T13:22:00Z")
  }
  ```
  
* JSON arrays can be generated by nesting a sequence of "item" attributes inside another element (the tag name "item" is reserved in this sense).
  ```XML
  <root>
    <hobbies>
      <item>chess</item>
      <item>sky-diving</item>
      <item>
        <name>reading</name>
        <last_practiced type="date">2015-02-22 07:00:00</last_practiced>
      </item>
    </hobbies>
  </root>
  ```
  translates to:
  ```javascript
  {
    "hobbies" : [ 
      "chess",
      "sky-diving",
      {
        "name" : "reading",
        "last_practiced" : ISODate("2015-02-22T07:00:00Z")
      }
    ]
  }
