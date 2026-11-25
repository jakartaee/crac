# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the **Jakarta CRaC** (Coordinated Restore at Checkpoint) specification project: a standard behaviour for Jakarta EE applications and runtimes for checkpoint and restore events. It is a multi-module Maven project with two modules, `api` and `spec`. The repository layout and build follow [Jakarta Agentic AI](https://github.com/jakartaee/agentic-ai); `tck` and `tck-dist` modules are expected to be added the same way once there is API to test.

## Build Commands

```bash
# Full build (what CI runs)
mvn clean install

# Specification document only (HTML, PDF and DocBook in spec/target/generated-docs)
mvn -pl spec package

# Format all sources (run before committing)
mvn spotless:apply
```

Java formatting is automated with Spotless (root pom) using palantir-java-format. Markdown, AsciiDoc, XML, properties, shell, Jenkinsfile and workflow YAML files are checked for trailing whitespace and a final newline. `spotless:check` runs in `verify`, so CI fails on unformatted files.

## Architecture

### API module (`api/`)

Defines the `jakarta.crac` package. It currently holds only `package-info.java`; the compiler runs with `-Xpkginfo:always` so the package exists in the jar. javac refuses to export an empty package, so there is no `module-info.java` yet and bnd sets `Automatic-Module-Name: jakarta.crac`. When the first type is added, add `module-info.java` (`module jakarta.crac { requires transitive jakarta.cdi; exports jakarta.crac; }`) and remove the `Automatic-Module-Name` line from `api/pom.xml`. Javadoc also fails on a package without types, while Maven Central requires a javadoc jar, so the `placeholder-javadoc` profile in `api/pom.xml` skips Javadoc and attaches a jar holding `src/main/javadoc-placeholder/README.md` instead. The profile is active only while `module-info.java` is missing, so adding it switches real Javadoc back on; then delete the profile and the placeholder directory.

### Specification module (`spec/`)

AsciiDoc sources in `spec/src/main/asciidoc`. `spec.asciidoc` is the entry point; it includes `license-efsl.adoc` (EFSL v2.0, do not edit the license text) and `jakarta-crac.adoc`, which includes the chapters in `chapters/`. Every heading carries an explicit `[[kebab-case]]` anchor so TCK tests can cite the specification section they verify. Sections that are not yet written hold a `NOTE: _To be written._` placeholder describing the intended content.

### Key constraints

- Java SE 21 and Jakarta EE 11 are the baseline, declared once in the root pom: `maven.compiler.release` (enforced by `maven-enforcer-plugin`) and `jakarta.ee.version`.
- Modules depend on the platform umbrella `jakarta.platform:jakarta.jakartaee-api`, declared with no `<version>` and no `<scope>`; both come from the root `dependencyManagement` (`provided`).
- `api` is published; `spec` is not. A module that should not be published needs the `maven.deploy.skip` and `skipPublishing` properties **and** a `stage-release` profile that configures `maven-deploy-plugin` with `<skip>true</skip>`, because the EE4J parent's `stage-release` profile overrides the property.
- CycloneDX SBOMs are generated for published modules only: `cyclonedx.skip` is `true` in the root pom and `false` in `api`.
- Every third-party dependency needs Eclipse IP approval; regenerate `DEPENDENCIES` after changing dependencies (see `CONTRIBUTING.md`).
