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

Quarkus switches effort from application startup time to compile time, e.g. some applications using XML as configuration need a huge amount of memory for XML parsing libraries: 
- that are only used once, on application startup, then not needed 
- this has a big impact on startup time and memory 
- So when you move this processing to compile-time, all of these XML parsing classes and bloat can be removed from the runtime.

There are numerous other similar optimisations Quarkus also does.

Quarkus leverages a lot of existing standards and functionality including Servlets, CDI etc. So you don’t need to learn a new language, like GO, to write cloud native apps.

And Quarkus brings joy to developers - through live code updates. No more long waits during application build compile etc. With Kogito and Quarkus, just save your file and it’s ready for test.

On the bottom of the next illustration, we can 3 bases of measurement
- traditional cloud ( effectively Spring Boot )
- Quarkus optimised JVM mode
- and the 3rd Compile to Native, allowing extremely low memory consumption and startup

![](https://raw.githubusercontent.com/tnscorcoran/kogito-demo/master/images/7.png)


Now to the demo. First live code updates. This is valuable becaus it brings JOY to developers - no more mvn compile, install package, whatever - waiting around for several seconds - or sometimes minutes.
When you save a file, in the background it’s compiled & available which truly does bring joy to developers and it makes them more productive

Our demo application is a simple process where we send a RESTful API call to it - and it decides
based on a Drools rule - whether that person is an adult or not - and returns that in a JSON Payload

OK the first part of the demo - live code updates.

We’re going to make a change to a source file _org.acme.kogito.model.Persons.java_, exposing a new field called employed 
which initially is commented out.

## Start in Developer mode
Clone this repo and nagivate to the root directory. Run

`./mvnw compile quarkus:dev`

We start in Developer mode - after a few seconds - it’s ready

Now we go over to POSTMAN and make this API call (curl also possible in a terminal)

`curl -X POST http://localhost:8080/persons \
    -H 'content-type: application/json' \
    -H 'accept: application/json' \
    -d '{"person": {"name":"John Quark", "age": 20}}'`

We can see that we have no employed field in the payload.

Now if we switch back to our IDE - uncomment the employed section at the bottoms of the file and save it
**NOTE, no maven compilation is needed**, make our API call again - we can see the employed field is returned

This is an absolutely awesome feature of Quarkus and Kogito


## JVM Mode
Now the second part of the demo. As we mentioned - Quarkus and Kogito provides big improvements over standard cloud native java - due to 
- its optimisations, 
- removal of dead code
- & ahead of time compilation

We’re going to compare this (already optimised) startup time and memory - in **_JVM_** mode
with startup time and memory - in **_NATIVE_** mode a little later

Stop the application running in Dev mode by pressing CTRL +  C. Then run
```
clear
./mvnw package
```

to build our jar. Now start it:
```
clear
java -jar ./target/using-kogito-1.0-SNAPSHOT-runner.jar
```

Record the startup time in the terminal window.

Now we're going to record our memory usage. We'll use Resident Set Size, or RSS. With the application still running, in a second terminal run:
```
clear
ps -o pid,rss,command -p $(pgrep -f runner)
```

Record the RSS value in the terminal window.


## Native Mode

In order to run in this mode, we need Graal VM installed and on our path. To do this following instructions here:  https://quarkus.io/guides/building-native-image-guide

First build the native application:
```
./mvnw package -Dnative
```
This may take several minutes to complete - recall we're now doing a lot of processing ahead of time at the compile stage so it's already done on application startup.

Now run the application in native mode:
```
clear
./target/using-kogito-1.0-SNAPSHOT-runner
```

Again, make the same nmeasurements of startup time and RSS memory.

You'll see a staggering difference - e.g. here's a sample of a couple of runs I did:
![](https://raw.githubusercontent.com/tnscorcoran/kogito-demo/master/images/11-measurements.png)

You can see that in Native mode my startup time was 80 times faster and memory consumption 23 times lower than already optimised JVM mode.

This truly is game changing - especially on the cloud and even more so with Serverless workloads which will soon proliferate, where low memory and startup times are critical.

Visit these links for more info:
- Kogito - https://kogito.kie.org/
- Quarkus - https://quarkus.io/

There is a recording of this demo at:



