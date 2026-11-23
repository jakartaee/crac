# Jakarta CRaC

Jakarta CRaC (Coordinated Restore at Checkpoint) defines a standard behaviour for Jakarta EE applications and runtimes for checkpoint and restore events.

## Background

The CRaC (Coordinated Restore at Checkpoint) Project researches coordination of Java programs with mechanisms to checkpoint (make an image of, snapshot) a Java instance while it is executing. Restoring from the image could be a solution to some of the problems with the start-up and warm-up times.

Jakarta CRaC defines how to make the runtime aware of a checkpoint being taken and when it is being restored. It also defines a way for application developers to give instructions to the runtime how to handle external resources used by the application.

## Goals

* Provide a standard mechanism to notify Jakarta EE implementations about checkpoint and restore events
* Provide a standard mechanism for Jakarta EE applications to make implementations aware of resources to manage at checkpoint and restore events
* Work seamlessly with CRaC and InstantOn

## Non-goals

* The specification does not seek to replace the existing [CRaC API](https://github.com/CRaC/org.crac)

## Version 1.0

The first release of Jakarta CRaC defines:

* The automatic checkpoint
* The manual checkpoint, triggered from outside the JVM (for example with `jcmd`)
* The obligations of the application server towards CRaC resources
* CDI events and annotations
* A TCK

## Target Platform

* Java SE 21 or higher
* Jakarta EE 11 or higher

## Community

Our mailing list is [crac-dev@eclipse.org](https://accounts.eclipse.org/mailing-list/crac-dev). The project page is [projects.eclipse.org/projects/ee4j.crac](https://projects.eclipse.org/projects/ee4j.crac) and the specification page is [jakarta.ee/specifications/crac](https://jakarta.ee/specifications/crac/).

## Directories

- [<b>api/</b>](api/): The API that applications program against
- [<b>spec/</b>](spec/): The specification document (AsciiDoc)

## Building

You can build all the modules at once:

```
mvn clean install
```

You can also build individual parts via Maven in their respective directories. Java formatting is checked by Spotless during `verify`; run `mvn spotless:apply` before committing.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on contributing to Jakarta CRaC.
