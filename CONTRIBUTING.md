# Contributing
We would love practical, unique, and inspiring samples to help developers tailor their own Dockerfiles to suit their needs.

## Rules
1. All contributions must install Visual Studio Build Tools.
2. All contributions must be text (dockerfiles, scripts, etc.).
3. All contributions must adopt the [MIT license](LICENSE.txt) at the top of each file (see [example](managed-native-desktop/Dockerfile)).
4. All contributions must be in a unique directory.
5. All contributions must have a README file explaining in generalized terms (i.e. no company secrets, but providing context on who you are or represents is optional and might be useful) what sort of workloads the Dockerfile supports (see [example](managed-native-desktop/README.md)).
6. All supporting files referenced within the Dockerfile must be text and included within the samples directory (see [example](managed-native-desktop/Install.cmd)).
7. All contributions must be tested and work if someone were to copy the files and run commands as described in your README.
8. All contributions must be easy to understand and must not be obfuscated. These are samples, and we want end users to be confident should they use these samples as a starting point for their pipeline.
9. Include a link to your README file in the root [README](README.md) sorted by its brief title.

## Template
Please consider the [.NET Framework + native desktop](managed-native-desktop/README.md) sample a template and author yours similarly.

## Review
The rules above will be enforced in pull request reviews and you may be asked to make changes. PRs that have not been fixed within 2 weeks may be abandoned. You can still make requested changes and re-submit at any time.

## Derivation
Contributors are encouraged to derive new, tested samples that provide significant value. If you believe you have found a problem, please open a new issue and @tag the author of the sample. Since all these samples should be tested, the author's feedback will be vital during the review process.
