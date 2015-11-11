------------------------------------
Hibiscus Payment-Server Docker Image
------------------------------------
Initial version by [miracle2k/dockerfiles](https://github.com/miracle2k/dockerfiles/)

[Hibiscus](http://www.willuhn.de/products/hibiscus-server/) communicates with
(German) banks using the HBCI/FinTS protocol.

Usage:

    $ docker run -e PASSWORD=foo -p 8080:8080 elsdoerfer/hibiscus-server

PASSWORD is the password used to encrypt the database.

The data directory is set to ``/srv/hibiscus``.

*Note*: The server seems to be hanging for multiple minutes on the log message ``[INFO][de.willuhn.jameica.sensors.service.impl.SchedulerImpl$Worker.run] collected data from device: hibiscus.server: statistics`` before finally booting up the web interface (wee https://github.com/willuhn/hibiscus.server/issues/2).

Database
--------

By default, an embedded database will be created within the data directory.

You may use PostgreSQL or MySQL instead by specifying some environment variables:

**DB_DRIVER**: ``postgres`` (default) or ``mysql``.

**DB_ADDR**, **DB_NAME**, **DB_USERNAME**, **DB_PASSWORD**: Connection info.

To initialize the database the first time, call ``initdb``:

    $ docker run -e DB_DRIVER=mysql ... run elsdoerfer/hibiscus-server initdb


Other supported environment values
----------------------------------

**USE_SSL** (default: false): Serve via SSL.

**PORT** (default: 8080): Port to provide service at.