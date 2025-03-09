# Romantic Versioning

Romantic Versioning (or RomVer) is inspired by [SemVer](https://semver.org/), but is meant to better fit the way that humans perceive version changes. You can see the 'official' RomVer repository [here](https://github.com/romversioning/romver).

<br>

## Definition

In short, RomVer is defined as `vPROJECT.MAJOR.MINOR[-lts][.FIX][-preX][+BUILD]`, where:

- `PROJECT` is incremented when there is a large conceptual change, essentially creating a new, separate project
- `MAJOR` is incremented when there are breaking changes
- `MINOR` is incremented when there are non-breaking changes
- `[-lts]` is an optional purely aesthetic addon if the release is designated for long-term support
- `[.FIX]` is an optional addon where FIX is incremented per fix for old releases (used mainly to prevent duplicate versions)
- `[-preX]` is an optional pre-release addon where X is incremented per pre-release per release
- `[+BUILD]` is an optional addon which differentiates copies of the contents of a release (only applicable for contents of a release and not a release itself)

<br>

## Why was this made?

This was made to fix the confusion that SemVer often creates regarding MAJOR changes. When a project releases a v2.0, people don't automatically think of it as a simple breaking change as they should, they think of it as being an extremely big deal. And conversely, when a project releases a v54.0, people don't automatically think of it as a simple breaking change as they should, they think of it as another small and tedious step that isn't noteworthy.

For whatever reason, humans seem to naturally put a lot of personal attachment in the first number of a version, and this standard attempts to work with that fact instead of overriding it. 

<br>

## Why should this be used?

#### - &nbsp; The specification is barely even needed, it basically just states what people already expect when looking at the three numbers.

#### - &nbsp; It conveys more information to users

- The MINOR and PATCH segments in SemVer are both backwards-compatible, so they're identical when it comes to whether or not users should update. Here, they're combined into a single segment.
- The PROJECT and MAJOR segments denote differing levels of breaking changes, with MAJOR increments likely being easy to update to and PROJECT increments likely being not easy to update to.

#### - &nbsp; It is possibly the least likely format to cause confusion and wrongful assumptions, as it is only attempting to standardize human intuition.

#### - &nbsp; It is compatible with systems that expect SemVer. This mainly uses three numerical segments, which makes it compatible with essentially every system that takes a version number, plus there are rules for how to compact a more complex version to just three integers.

#### - &nbsp; (Extra) It can be used for projects of all types, even for projects whose users may not be tech-savvy. This standard is extremely intuitive, so users don't have to read a technical specification meant for developers.

#### - &nbsp; (Extra) You don't have to do something crazy like "Project v2 v0.1.0" if you want to radically transform your project.

<br>
<br>
<br>

## RomVer Specification v1.1.0:

<br>

1: &nbsp; The 'RomVer Format' is defined as "vPROJECT.MAJOR.MINOR\[-ltsX]\[.FIX]\[-preX]\[+BUILD]", where "PROJECT", "MAJOR", and "MINOR" are each positive integers, "\[-lts]" (without the brackets) is an optional purely aesthetic segment to designate long-term support, "\[.FIX]" (without the brackets) is an optional segment where "FIX" is a positive integer, "\[-preX]" (without the brackets) is an optional segment for pre-release versions where "X" is a positive integer, and "\[+BUILD]" (without the brackets) is an optional segment only applied to specific variations of a release's contents where "BUILD" is composed only of numbers, letters, periods, and dashes. The leading "v" may be omitted.

2: &nbsp; A 'Version' is defined as an ASCII string that follows the RomVer Format without a 'BUILD' segment.

3: &nbsp; A 'Build Version' is defined as an ASCII string that follows the RomVer Format with a 'BUILD' segment.

4: &nbsp; If a 'Project' wishes to use the RomVer standard, it must adhere every following rule:

5: &nbsp; Each release of the Project must have a unique version, one or more variations of contents derived from the Project, a sufficient entry in a changelog for the Project, and clear and comprehensive documentation for any and all interfaces provided by the contents of the release.

6: &nbsp; The contents (counted recursively) of each release of the Project must remain strictly unchanged in every possible manner once released, as much as relevant systems will allow. If the contents of a release require change, the change must be issued as a new release.

7: &nbsp; The Version for the first release of the Project must be "v0.1.0" if the project is considered unfit for stable use, or "v1.0.0" if it is considered fit for stable use.

8: &nbsp; Each Version of each release (or the 'New Release') of the Project must be based off the Version of whichever (non preview) release the New Release was based on (or the 'Old Release'), and must differ according to these rules:

&nbsp; &nbsp; &nbsp; 8.1: &nbsp; If the Old Release is not the latest release, the Version of the New Release must be the Version of the Old Release plus a ".FIX" segment where "FIX" is a number which starts at 1 and is incremented per fix release for the original non-fix release.

&nbsp; &nbsp; &nbsp; 8.2: &nbsp; Otherwise, if the New Release is a preview for a 'Planned Future Release', the Version must be the expected Version of the Planned Future Release plus a "-preX" segment where "X" is a number which starts at 1 and is incremented for each preview release for the Planned Future Release. If the version of the Planned Future Release changes in a way that would cause a duplicate pre-release Version (ignoring "-lts" segments), the New Release must continue incrementing "X" from the older release it would otherwise clash with.

&nbsp; &nbsp; &nbsp; 8.3: &nbsp; Otherwise, if the New Release is to be considered as a separate project from the Old Release, or if the New Release is considered fit for stable use and the Old Release is not, the PROJECT segment of the Version must be incremented and the MAJOR and MINOR segments must be reset to 0.

&nbsp; &nbsp; &nbsp; 8.4: &nbsp; Otherwise, if users might encounter breaking changes compared to the Old Release, the MAJOR segment of the Version must be incremented and the MINOR segment must be reset to 0, but the PROJECT segment must stay the same.

&nbsp; &nbsp; &nbsp; 8.5: &nbsp; Otherwise, the MINOR segment must be incremented, but the PROJECT and MAJOR segments must stay the same.

&nbsp; &nbsp; &nbsp; 8.6: &nbsp; Additionally, if the New Release is designated for long-term support (or LTS), the Version must include an "-lts" segment.

9: &nbsp; If a release contains multiple differing copies of the released data, each copy may include its own Build Version which must be the same as its release's version plus a "+BUILD" segment which must be unique from all other "+BUILD" segments in the release.

10: &nbsp; Ordering of two Versions is determined by comparing the PROJECT segments if they differ. Otherwise, the MAJOR segments are compared if they differ. Otherwise, the MINOR segments are compared if they differ. Otherwise, the pre-release segments are compared if they differ, with no pre-release segment being the greatest. Otherwise, the versions are equivalent. The presence (or lack thereof) of an LTS segment does not affect ordering.

11: &nbsp; If a Version has to be converted to just 3 positive integers for use in existing systems, the components must be calculated as `(PROJECT + (1000 if LTS) + (10,000 * pre-release number (or 0))), MAJOR, MINOR + 10,000 * fix number (or 0)`. Some examples of Versions and their associated three-integer formats:
- "v1.2.3" -> "1,2,3"
- "v1.2.3.4" -> "1,2,40003"
- "v2.0.0-pre2" -> "20002,0,0"
- "v1.5.2-lts" -> "1001,5,2"
- "v1.5.2-lts.4" -> "1001,5,40002"
- "v1.5.2-lts-pre1" -> "11001,5,2"
- "v1.5.2-lts.5-pre1" -> "11001,5,50002".

<br>

## Notes

- The definition of "considered a separate project" must be subjectively interpreted by each project maintainer, but that is the only area where subjectivity is allowed.
- It is assumed that versions should never be labeled as alphas or betas and that v0.x.x should always be used instead.
- It is assumed that build versions should never be converted to a three-integer format.
- This repository has been dedicated to the public domain with the [CC0 license](LICENSE).
