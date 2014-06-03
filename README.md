This will be possible through the webapp interface soon !

Synopsx
=======


Full XML corpus publishing system developped at ENS Lyon (http://ahn.ens-lyon.fr) based on BaseX

Installation
------------
```bash
    cd <path_to_basex>/
    rm -fr webapp
    rm -fr repo
    git clone https://github.com/ahn-ens-lyon/synopsx.git .
```

Don't forget to change your admin password !


Configuration
-------------

### Default syntax

If you use the BaseX Client use the default syntax : http://docs.basex.org/wiki/Commands
You can also use the command line syntax : http://docs.basex.org/wiki/REST#Command_Line


#### Config database

`CREATE DB 'config'` create the config database (http://docs.basex.org/wiki/Commands#CREATE_DB)

`OPEN DB 'config'` open the config database (http://docs.basex.org/wiki/Commands#OPEN_DB)

`ADD synopsx.xml` add the config file  (http://docs.basex.org/wiki/Commands#ADD)

```xml
    <configuration name="synopsx">
        <output name="xhtml" value="synopsx"/>
        <output name="oai" value="oai"/>
    </configuration>
```

#### Project database

`CREATE DB 'myproject'`

`OPEN DB 'myproject'`

`ADD myproject_data.xml` (or ADD TO 'myproject/' myproject_data.zip)

`OPEN DB 'config'`

`ADD myproject.xml`

```xml
    <!-- config file for 'myproject' -->
    <configuration name="myproject">
        <!-- The @value attribute gives the parent xqm module name -->
        <parent value="parent-module-name"/>  
        <!-- The @value attribute gives the output xqm module name -->
        <output name="xhtml" value="myproject-xhtml-module-name"/>  
        <!-- Uncomment this line to overwrite synopx oai default functions -->
        <!--<output name="oai" value="myproject-xhtml-module-name"/>-->
    </configuration>
```

### XQuery syntax

You can also interact with BaseX with the XQuery syntax for the installation process : http://docs.basex.org/wiki/Database_Module

#### Config database

```xquery
    <!-- create the config database (http://docs.basex.org/wiki/Database_Module#db:create) -->
    db:create("config")
```

```xquery
    <!-- open the config database (http://docs.basex.org/wiki/Database_Module#db:open) -->
    db:open("config")
```

```xquery
    <!-- add the XML sequence to the config database (http://docs.basex.org/wiki/Database_Module#db:add) -->
    db:add("config",
    <configuration name="synopsx">
        <output name="html" value="synopsx_html"/>
        <output name="oai" value="synopsx_oai"/>
    </configuration>, "synopsx.xml" )
```

#### Project database

```xquery
    <!-- create the project database (http://docs.basex.org/wiki/Database_Module#db:create) -->
    db:create("myproject")
```

```xquery
    <!-- open the project database (http://docs.basex.org/wiki/Database_Module#db:open) -->
    db:open("myproject")
```

```xquery
<!-- Add XML data to the project database -->


```



```xquery
    <!-- add the project's config XML sequence to the config database (http://docs.basex.org/wiki/Database_Module#db:add)

    first open the config database (http://docs.basex.org/wiki/Database_Module#db:open) -->

    db:open("config")

    db:add("config",
    <configuration name="myproject">
        <!-- The @value attribute gives the parent xqm module name -->
        <parent value="parent-module-name"/>  
        <!-- The @value attribute gives the output xqm module name -->
        <output name="xhtml" value="myproject-xhtml-module-name"/>  
        <!-- Uncomment this line to overwrite synopx oai default functions -->
        <!--<output name="oai" value="myproject-xhtml-module-name"/>-->
    </configuration>, "myproject.xml" )
```
