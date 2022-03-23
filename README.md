# onvif-java-webservices
Based on https://github.com/fpompermaier/onvif with updates to latest versions of WSDLs (dec '21)

# Java ONVIF (Open Network Video Interface Forum)

ONVIF is a community to standardize communication between IP-based security products (like cameras).

This project aims to improve https://github.com/milg0/onvif-java-lib.

Apported improvements
=============
* Project **mavenization** and **modularization** (separation between Java stubs and application) and 
* WS client generation using Apache CXF maven plugin (declaring the specific Onvif specification of each wsdl)
* maintainability and extendability of the overall code
* Separation of Test/examples from other code

Rebuilding WS stubs
=============

If you need to change the list of managed WSDLs (in onvif/onvif-ws-client/src/main/resources/wsdl) and thus you need to regenerate the WS Java stubs using the [Apache CXF codegen maven plugin](http://cxf.apache.org/docs/maven-cxf-codegen-plugin-wsdl-to-java.html), you need to go through the following steps:
 1. **Download Onvif WSDLs** to onvif/onvif-ws-client/src/main/resources/wsdl appending the version before the .wsdl suffix.
 For example, from main dir (onvif) use you can run the following shell commmand:<br>
```wget http://www.onvif.org/onvif/ver10/device/wsdl/devicemgmt.wsdl onvif-ws-client/src/main/resources/wsdl/devicemgmt_2.5.wsdl ```
 1. **Update WSDLLocations constants (if needed)** within class  *de.onvif.utils.WSDLLocations* (module onvif-java)
 1. **Add required url-rewriting rules (if needed)** to onvif/onvif-ws-client/src/main/resources/wsdl/jax-ws-catalog.xml
 1. Delete old Java classes in onvif/onvif-ws-client/src/main/java
 1. **Run the class generation command**: decomment goal and phase of cxf-codegen-plugin in onvif-ws-client pom.xml and run ```mvn clean install```
 1. To see how to properly add a new ONVIF service to OnvifDevice look into OnvifDevice.init()
