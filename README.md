This is my own attempt at creating a good and solid specification for [Romantic Versioning](https://github.com/romversioning/romver).



# Romantic Versioning

Romantic Versioning (or RomVer) is inspired by [SemVer](https://semver.org/), but is meant to better fit the way that humans naturally perceive version changes

<br>

## Definition

In short, RomVer is defined as `vPROJECT.MAJOR.MINOR[-lts][-preX]`, where:

- `PROJECT` is incremented when there is a large conceptual change, essentially creating a new, separate project
- `MAJOR` is incremented when there are breaking changes
- `MINOR` is incremented when there are non-breaking changes
- `[-lts]` is an optional purely aesthetic addon if the release is meant for long-term support
- `[-preX]` is an optional pre-release addon where X is incremented per pre-release per release

<br>

## Why was this made?

This was made to fix the confusion that SemVer often creates regarding MAJOR changes. When a project releases a v2.0, people don't automatically think of it as a simple breaking change as they should, they think of it as being an extremely big deal. And conversely, when a project releases a v54.0, people don't automatically think of it as a simple breaking change as they should, they think of it as another small tedious step that isn't noteworthy.

<br>

## Why should this be used?

- 1: It is very intuitive for everyone involved (users, maintainers, etc)
- 2: It is compatible with systems that expect SemVer
- 3: It is possibly the least likely format to cause confusion and wrongful assumptions

<br>
<br>
<br>

## RomVer Specification v1.0.2:

<br>

1: &nbsp; The 'RomVer Format' is defined as "vPROJECT.MAJOR.MINOR\[-lts]\[-preX]", where "PROJECT", "MAJOR", and "MINOR" are each placeholders for positive integers, "\[-lts]" (without the brackets) is an optional purely aesthetic segment for long-term support, and "\[-preX]" (without the brackets) is an optional segment for pre-release versions, where X is a placeholder for a positive integer.

2: &nbsp; A 'Version' is defined as an ASCII string that follows the RomVer Format, even if the leading "v" is omitted.

3: &nbsp; If a 'Project' wishes to follow the RomVer standard, it must follow every following rule:

4: &nbsp; Each release of the Project must have exactly one Version attached, and that Version must never change for said release.

5: &nbsp; Each release must have all its notable changes listed in a changelog, and if the release has a public api, said api must be clearly and comprehensively documented.

6: &nbsp; The contents (counted recursively) of each release of the Project must remain strictly unchanged in every possible manner once released, as much as relevant systems will allow. If the contents of a release require change, the change must be issued as a new release.

7: &nbsp; The Version for the first release of the Project must be "v0.1.0" if the project is considered unfit for stable use, or "v1.0.0" if it is considered fit for stable use.

8: &nbsp; Each Version of each release (or the New Release) of the Project must be based off the Version of whichever (non preview) release the New Release was based on (or the Old Release), and must differ according to these rules:

&nbsp; &nbsp; &nbsp; 8.1: &nbsp; If the New Release is a preview for a 'Planned Future Release', the Version must be the expected Version of the Planned Future Release concatenated with "-pre" and a number which starts at 1 and is incremented for each preview release for the Planned Future Release.

&nbsp; &nbsp; &nbsp; 8.2: &nbsp; Otherwise, if the New Release is to be considered as a separate project compared to the Old Release, or if the New Release is considered fit for stable use and the Old Release is not, the PROJECT segment of the Version must be incremented and the MAJOR and MINOR segments must be reset to 0.

&nbsp; &nbsp; &nbsp; 8.3: &nbsp; Otherwise, if users might encounter breaking changes compared to the Old Release, the MAJOR segment of the Version must be incremented and the MINOR segment must be reset to 0, but the PROJECT segment must stay the same.

&nbsp; &nbsp; &nbsp; 8.4: &nbsp; Otherwise, the MINOR segment must be incremented, but the PROJECT and MAJOR segments must stay the same.

&nbsp; &nbsp; &nbsp; 8.5: &nbsp; Additionally, if the New Release is meant for long-term support (or LTS), the Version must include "-lts" directly after the MINOR segment.

9: &nbsp; Ordering between two Versions is determined by comparing the PROJECT segments if they differ. Otherwise, the MAJOR segments are compared if they differ. Otherwise, the MINOR segments are compared if they differ. Otherwise, the pre-release segments are compared if they differ, with no pre-release segment being the greatest. Otherwise, the versions are equivalent. The presence (or lack thereof) of an LTS segment does not affect ordering.

10: &nbsp; If a Version has to be converted to just 3 positive integers for use in existing systems, the first component must be calculated as `(PROJECT + (1000 if LTS) + (10,000 * pre-release number (or 0)))`. The second and third components must be the MAJOR and MINOR segments, respectively. For example, "v1.2.3" would be "1,2,3", "v2.0.0-pre2" would be "20002,0,0", "v1.5.2-lts" would be "1001,5,2", and "v1.5.2-lts-pre1" would be "11001,5,2".

<br>

## Notes

- The definition of "considered a separate project" must be subjectively interpreted by each project maintainer, but that is the only area where subjectivity is allowed.
- There are many times when you can and should have releases that do not strictly increase the version number compared to the latest release (such as fixes for versions of the project which are older but still supported).
- Concepts like release alphas and betas are not recognized by this format.
- All releases, no matter how small, must at least increment the MINOR segment or the pre-release segment.
- Additional data like build metadata, release date, etc. should not be included in the version.
- This repository has been dedicated to the public domain with the [CC0 license](LICENSE).
