# Jakarta CRaC

Jakarta CRaC (Coordinated Restore at Checkpoint) defines a standard behaviour for Jakarta EE applications and runtimes for checkpoint and restore events.

## Jakarta CRaC Specification

This module contains the AsciiDoc sources and configuration to generate the Jakarta CRaC specification documentation in HTML and PDF formats under the Eclipse Foundation Specification License (EFSL) v2.0.

The entry point is `src/main/asciidoc/spec.asciidoc`, which includes the license and `jakarta-crac.adoc`, which in turn includes the chapters in `src/main/asciidoc/chapters/`.

## Building Documentation

To build the specification documentation:

```
mvn clean package
```

The generated documentation will be found in `target/generated-docs/`.
