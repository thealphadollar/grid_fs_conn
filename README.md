# grid_fs_conn

A Grid FS Connector to ease uploading files with metadata to mongoDB and searching / retrieving them later; providing a workaround to the limitations of mongo DB and easy integration with REST API.

## Installing

The package is [available using npm](https://www.npmjs.com/package/grid_fs_conn_ssrx).

`npm i grid_fs_conn_ssrx`

## What It Does

The package aims at solving the problem of saving large `tiff` or `PDF` files inside Mongo Databases. The package provides an easy to use API using which one can leverage `GridFS` method to store files inside a mongo database.

Read more about the mongo database's gridFS [here](https://docs.mongodb.com/manual/core/gridfs/).

## What is the API

The package exposes the class `GridFSConnector` which has the following methods for usage. The methods below are designed to be used with a REST API and hence take in `response` object as parameter wherever a result has to be returned.

- GridFSConnector(DB_URI): Main class to be constructed with MongoDB URI.
- GridFSConnector.uploadFax(objs): Pass in the list of objects to be stored. The objects should have the structre defined alter on.
- GridFSConnector.searchFax(query, res): Pass in the query as a JSON (example `{"field1" : "value", "field2": "value"}`) and the response object where to return the JSON result with.
- GridFSConnector.downloadFax(fileName, res): Pass in the filename as a string and the response object where to return the binary data with.
- GridFSConnector.getFaxMetadata(fileName, res): Pass in the filename as a string and the response object where to return the metadata JSON result with.

### Structure of object

The structure of each object should be as follows in the very least. Other data can be present in the object which will be saved as it's metadata.

```JSON
{
    DocumentParams: {
        Type: "MIMETYPE",
        Hash: "HASH",
        FaxImage: "BASE64 STRING OF THE FILE TO BE STORED"
    }
}
```

Note:

- The filename is the value present in `DocumentParams.Hash` attribute of the object passed in.
- The file binary data is passed as a base64 string in `DocumentParams.FaxImage`
- Entire object JSON excluding the `DocumentParams.FaxImage` is stored as the metadata for the file and can be retrieved later.

## Customizing the package

The package is easily customizable as modular coding practices have been used. Contributors are welcome to different versions of the same as well as add more features to the existing package.

For any queries or suggestions please reach at code@thealphadollar.me
