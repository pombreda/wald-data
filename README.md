
wald-storage
============

wald-storage is built on various third-party components:

- Fuseki is used as a database
- Redis is used to mint identifiers
- A Linked Data Fragments server is used as a read-only webservice to the database

Follow the instructions below to set things up.


Step 1.  Install and configure all your requirements
----------------------------------------------------

First, make sure you have java, redis, node.js and python installed. If you're on an older
Ubuntu you may have to use the
[chris lea PPA](https://launchpad.net/~chris-lea/+archive/ubuntu/node.js) to install node.js.
The other requirements can be installed with:

    sudo apt-get install openjdk-7-jdk redis-server
    sudo apt-get install python-virtualenv python-pip
    bin/bootstrap

The bootstrap script will install various third-party python libraries in a virtualenv.  It will
also download Fuseki and the node.js [Linked Data Fragments](http://linkeddatafragments.org/software/)
server. [Fuseki](https://jena.apache.org/documentation/serving_data/) is the SPARQL server included
in the Apache Jena project.


____ FIXME: everything below this line is outdated ____






Step 2. Creating your dataset
-----------------------------

To initialize the database you will have to decide on the name of the dataset for your
project. In the future wald:meta will support multiple datasets in one deployment, but currently
only one is supported.  The dataset name will be used as an identifier in various places, so
should a simple lowercase ascii string without special characters, i.e. it should match this
regex: /^[a-zA-Z][a-zA-Z0-9.-]*$/.  wald:meta will always create a "meta" dataset for your
wald:meta install which will contain user accounts and permissions.

You also need a base url to indicate at what location your project will be made available, the
base url will be used to mint various identifiers.  For example, if you have a dataset called
"books" and https://example.com/library as a base url, the following API roots will be available:

- https://example.com/library/books/dataset (Your book database)
- https://example.com/library/books/edits (History of changes made to your book database)
- https://example.com/library/meta/dataset (Metadata necessary to interact with your book database)
- https://example.com/library/meta/edits (History of changes made to the metadata)

To initialize your dataset run bin/init:

    bin/init <base url> <dataset>

All done, start the service!

    bin/service

NOTE: if you want to use multiple datasets, specify them as a comma separated list, e.g.:

    bin/init https://example.com/library books,music,movies


License
=======

Copyright (C) 2014  Kuno Woudt <kuno@frob.nl>

This program is free software: you can redistribute it and/or modify
it under the terms of copyleft-next 0.3.0.  See [LICENSE.txt](LICENSE.txt).

