# tMongoDBXMLOutput

This is a custom component for Talend Open Studio, Big Data Edition
6.0.1, which lets you write XML documents directly to MongoDB,
converting them into JSON. While Talend has excellent features to
construct complex XML documents, its JSON features are not quite on
par with that. This component allows you to construct your document
structure as XML and then automatically translate it to JSON the way
MongoDB expects it. In particular, this allows you to have multiple
arrays in the same document, while Talend's MongoDB components can
only deal with a single array. It is also possible to generate all
JSON data types that MongoDB supports.





