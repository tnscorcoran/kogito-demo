# Kogito Demo

## Introduction - Kogito and Quarkus. 

This repo covers a demo on Kogito - the new Red Hat sponsored open-source framework for business automation including
- Rules and Decisions 
- Processes and Cases

The origin of the word Kogito is - from the phrase by Rene Descartes
_Cogito, ergo sum_ meaning, _I think - therefore I am_

![](https://raw.githubusercontent.com/tnscorcoran/kogito-demo/master/images/2.png)

The 'c' was replaced with a 'k' as a reference to Kubernetes, the target cloud platform - where this framework is most applicable

though this demo is on my laptop - just to show the 3 big benefits of Kogito:
- fast startup
- low memory usage
- live code updates

![](https://raw.githubusercontent.com/tnscorcoran/kogito-demo/master/images/3-4-5-6.png)

Under the covers Kogito uses Quarkus, a Red Hat sponsored open-source Java framework for fast and lightweight Java applications.

Quarkus switches effort from application startup time to compile time

e.g. some applications using XML as configuration need a huge amount of memory for XML parsing libraries 
- that are only used once, on application startup, then not needed 
- this has a big impact on startup time and memory 
- So when you move this processing to compile-time, all of these XML parsing classes and bloat can be removed from the runtime.

there are numerous other similar optimisations Quarkus also does.

Quarkus leverages a lot of existing standards and functionality including Servlets, CDI etc. So you don’t need to learn a new language, like GO, to write cloud native apps.

And Quarkus brings joy to developers - through live code updates. No more long waits during application build compile etc. With Kogito and Quarkus, just save your file and it’s ready for test.

On the bottom of the next illustration, we can 3 bases of measurement
- traditional cloud ( effectively Spring Boot )
- Quarkus optimised JVM mode
- and the 3rd Compile to Native, allowing extremely low memory consumption and startup

![](https://raw.githubusercontent.com/tnscorcoran/kogito-demo/master/images/7.png)









