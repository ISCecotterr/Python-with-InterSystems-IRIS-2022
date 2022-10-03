# 1. Using Python with InterSystems IRIS
Presented at UK&I Summit, October 2022.
Demo showing various ways to use Python with InterSystems IRIS Data Platform:
* Embedded Python (available for 2021.2 +)
* DB-API (available for 2022.1 +)
* Python Gateway
* IRIS Native API

Thanks go to Guillaume Rongier @grongierisc for his many Python demos, upon which this was built, as well as Raj Singh @isc-rsingh for some sample code from his Global Summit 2022 presentation on the subject.

# 2. Starting this demo:
Please ensure you have Docker Desktop and Git installed wherever you wish to run this demo. This guide will assume you are using Visual Studio Code with the Docker Extension installed.

``` git clone https://github.com/ISCecotterr/iris-python-demo ```

Then in your cloned directory:

``` docker-compose up -d ```

In VS Code Docker Extension, right-click the container "iris-python-demo" and choose to "Attach Shell".

Now you can use the command line in the container and use ```irissession IRIS``` to access the IRIS terminal, and run ObjectScript commands.

To view the Management Portal, go to http://localhost:52775/csp/sys/UtilHome.csp and login with username: _System, password: SYS

# 3. Exploring this demo:
The *src > Python* directory contains the .py scripts used for the various examples.

The *src > ObjectScript* directory similarly contains the classes needed to support these.

## 3.1. Embedded Python
*src > ObjectScript > Embedded > Python.cls*

This class contains a large selection of Class and Instance Methods written in Python with ObjectScript wrappers. These can of course be called from the IRIS terminal, for example:

```do ##class(ObjectScript.Embedded.Python).HelloWorld("GitHub User")```

Documentation: https://docs.intersystems.com/irislatest/csp/docbook/DocBook.UI.Page.cls?KEY=AFL_epython 

## 3.2. DB-API
*src > Python > db-api > dbapi.py*

This .py demonstrates how to:
* Create DB-API connection to IRIS
* Create a table with a cursor object
* Generate data in Python and insert with SQL

To run this, go to the container command line and run:
1. ```cd /src/Python/db-api```
2. ```python3 dbapi.py```

You can view the results of the script in the System Explorer tab of the Management Portal.

## 3.3. Python Gateway
*src > ObjectScript > Gateway > Python.cls*

The Demo() ClassMethod of this Class shows step-by-step how to:
* Create a Python Gateway connection to IRIS
* Add a .py file to the Gateway paths
* Create proxy objects from Python objects
* Access properties of the proxy objects with ObjectScript

To run this, go to the container command line and run:
1. ```irissession IRIS```

Ensure you are in the USER namespace with ```set $namespace = "USER"```

2. ```do ##class(Gateway.Python).Demo()```

You can then exit the IRIS terminal with ```halt```

## 3.4. Native API
*src > Python > native > mindmap.py*

*src > Python > native > openID.py*

The mindmap.py code shows how to:
* Create a Native API connection to IRIS
* Write JSON to Globals, with a defined structure

The openID.py code writes the Globals.

To run this, go to the container command line and run:
1. ```cd /src/Python/native```
2. ```python3 openID.py```
3. ```python3 mindmap.py```
4. ```python3 openID.py```