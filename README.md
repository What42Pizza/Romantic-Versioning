This is my own attempt at creating a good and solid specification for [Romantic Versioning](https://github.com/romversioning/romver).



# Romantic Versioning

Romantic Versioning (or RomVer) is inspired by [SemVer](https://semver.org/), but is meant to better fit the way that humans naturally perceive version changes

<br>

## Definition

In short, RemVer is defined as `vHUMAN.MAJOR.MINOR[-lts][-preX]`, where:

- `HUMAN` is incremented when there is a large conceptual change
- `MAJOR` is incremented when there are breaking changes
- `MINOR` is incremented when there are non-breaking changes
- `[-lts]` is an optional addon if the release is meant for long-term support
- `[-preX]` is an optional pre-release addon where X is incremented per per-release per release

<br>

## Why was this made?

This was made to fix the confusion that SemVer often creates regarding MAJOR changes. When a project releases a v2.0, people don't automatically think of it as a simple breaking change as they should, they think of it as being an extremely big deal. And conversely, when a project released a v54.0, people don't automatically think of it as a simple breaking change as they should, they think of it as another small tedious step that isn't noteworthy.

<br>

## Why should this be used?

- 1: It is very intuitive for everyone involved (users, maintainers, etc)
- 2: It is compatible with systems that expect SemVer
- 3: It is possibly the least likely format to cause confusion and wrongful assumptions

<br>
<br>
<br>

## Formal specification v0.1.1:

<br>

1: &nbsp; The 'RomVer Format' is defined as "vHUMAN.MAJOR.MINOR\[-lts]\[-preX]", where "HUMAN", "MAJOR", and "MINOR" are each placeholders for positive integers, "\[-lts]" (without the brackets) is an optional segment for long-term support, and "\[-preX]" (without the brackets) is an optional segment for pre-release versions, where X is a placeholder for a positive integer.

2: &nbsp; A 'Version' is defined as an ASCII string that follows the RomVer Format, even if the leading "v" is omitted.

3: &nbsp; If a 'Project' wishes to follow the RomVer standard, it must follow every following rule:

4: &nbsp; Each release of the Project must have exactly one Version attached and must have all its notable changes listed in a changelog.

5: &nbsp; The contents (counted recursively) of each release of the Project must remain strictly unchanged in every possible manner once released, as much as relevant systems will allow. If the contents of a release require change, the change must be issued as a new release.

6: &nbsp; The Version for the first release of the Project must be "v0.1.0" if the project is considered unfit for stable use, or "v1.0.0" if it is considered fit for stable use.

7: &nbsp; Each Version of each release (or the New Release) of the Project must be based off the Version of whichever release the New Release was based on (or the Old Release), and must differ according to these rules:

&nbsp; &nbsp; &nbsp; 7.1: &nbsp; If the New Release is considered significantly different in a conceptual sense compared to the Old Release, or if the New Release is considered fit for stable use and the Old Release is not, the HUMAN segment of the Version must be incremented and the MAJOR and MINOR segments must be reset to 0.

&nbsp; &nbsp; &nbsp; 7.2: &nbsp; Otherwise, if users might encounter breaking changes compared to the Old Release, the MAJOR segment of the Version must be incremented and the MINOR segment must be reset to 0, but the HUMAN segment must stay the same.

&nbsp; &nbsp; &nbsp; 7.3: &nbsp; Otherwise, the MINOR segment must be incremented, but the HUMAN and MAJOR segments must stay the same.

8: &nbsp; If applicable, the RomVer Format must be extended in the following ways:

&nbsp; &nbsp; &nbsp; 8.1: &nbsp; If a release is meant for long-term support (or LTS), its Version must be concatenated with "-lts".

&nbsp; &nbsp; &nbsp; 8.2: &nbsp; If a release is a preview for a 'Planned Future Release', its Version must be the expected Version of the Planned Future Release concatenated with "-pre" and a number which starts at 1 and is incremented for each preview release for the Planned Future Release.

9: &nbsp; Precedence between two Versions is determined by comparing the HUMAN segments, or if the HUMAN segments are equal then the MAJOR segments are compared, or if the MAJOR segments are equal then the MINOR segments are compared, or if the MINOR segments are equal the the pre-release segments are compared, with no pre-release taking precedence over all pre-release numbers, or if the pre-release segments are equal then the versions are the same. The presence (or lack thereof) of an LTS segment does not affect precedence.

10: &nbsp; If a Version has to be converted to just 3 positive integers for use in existing systems, the first component must be the HUMAN segment plus 1000 if it is LTS plus the pre-release segment (or 0 if not available) times 10,000, and the second and third segments must be the MAJOR and MINOR segments respectfully.

<br>

## Notes

- Concepts like release alphas and betas are not recognized by this format
- There are many times when you can and should have releases that do not strictly increase the version number compared to the latest release (such as fixes for versions of the project which are older but still supported)
- Additional data like build metadata, release date, etc. should not be included in the version
- This repository has been dedicated to the public domain with the [CC0 license](LICENSE)
