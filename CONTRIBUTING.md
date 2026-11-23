# Contributing to Jakarta CRaC

Thanks for your interest in Jakarta CRaC.

## Project description

Jakarta CRaC defines a standard behaviour for Jakarta EE applications and
runtime for checkpoint and restore events. It defines how to make the
runtime aware of a checkpoint being taken and when it is being restored,
and a way for application developers to give instructions to the runtime
how to handle external resources used by the application.

* https://projects.eclipse.org/projects/ee4j.crac

## Terms of Use

This repository is subject to the Terms of Use of the Eclipse Foundation

* https://www.eclipse.org/legal/termsofuse.php

## Developer resources

Information regarding source code management, builds, coding standards,
and more.

* https://projects.eclipse.org/projects/ee4j.crac/developer

The project maintains the following source code repositories

* https://github.com/jakartaee/crac

## Eclipse Development Process

This Eclipse Foundation open project is governed by the Eclipse Foundation
Development Process and operates under the terms of the Eclipse IP Policy.

## Specifications

This specification project operates under the terms of the Eclipse
Foundation Specification process.

* https://eclipse.org/projects/dev_process
* https://www.eclipse.org/org/documents/Eclipse_IP_Policy.pdf
* https://www.eclipse.org/projects/efsp/
* https://www.eclipse.org/legal/efsp_non_assert.php

## Eclipse Contributor Agreement

In order to be able to contribute to Eclipse Foundation projects you must
electronically sign the Eclipse Contributor Agreement (ECA).

* https://www.eclipse.org/legal/ECA.php

The ECA provides the Eclipse Foundation with a permanent record that you
agree that each of your contributions will comply with the commitments
documented in the Developer Certificate of Origin (DCO). Having an ECA on
file associated with the email address matching the "Author" field of your
contribution's Git commits fulfils the DCO's requirement that you sign-off
on your contributions.

For more information, please see the Eclipse Committer Handbook:
https://www.eclipse.org/projects/handbook/#resources-commit

## Dependencies

Every third-party dependency needs Eclipse IP approval, and `DEPENDENCIES` at
the repository root is the manifest the Eclipse Dash license check generates
from the build. CI runs the check on every push and fails if a dependency is
restricted or needs review, or if the committed `DEPENDENCIES` differs from
the generated one.

After changing dependencies, regenerate the manifest and commit it:

    mvn org.eclipse.dash:license-tool-plugin:license-check -Pdash-licenses -Ddash.summary=DEPENDENCIES

If the Dash API times out, the plugin leaves `DEPENDENCIES` truncated; restore
it with `git checkout -- DEPENDENCIES` and run again. A failed CI run uploads
the generated file as the `DEPENDENCIES` artifact. Review of a dependency is
requested at https://gitlab.eclipse.org/eclipsefdn/emo-team/iplab/-/issues.

## Contact

Contact the project developers via the project's "dev" list.

* https://accounts.eclipse.org/mailing-list/crac-dev
