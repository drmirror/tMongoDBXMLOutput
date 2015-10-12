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

(to be continued)




