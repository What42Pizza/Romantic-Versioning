This is my own attempt at creating a solid specification for [Romantic Versioning](https://github.com/romversioning/romver).



## Definition

Romantic Versioning (or RomVer) is inspired by [SemVer](https://semver.org/), but is made to better fit the way that humans naturally percieve versioning semantics and changes. In short, RemVer is defined as `vHUMAN.MAJOR.MINOR`, where HUMAN is incremented when there is a large conceptual change, MAJOR is incremented when there are breaking changes, and MINOR is incremented when non-breaking changes are made.

<br>

## Why was this made?

This was made because of the confusion SemVer often creates regarding MAJOR changes. When a project releases a v2.0, people don't automatically think of it as a simple breaking change as they should, they think of it as being an extremely big deal. And conversely, when a project released a v54.0, people don't automatically think of it as a simple breaking change as they should, they think of it as another small tedious step that isn't noteworthy.

<br>

## Why should this be used?

- 1: It is very intuitive for everyone involved
- 2: It is compatible with systems that expect SemVer (expect for the extended specification)
- 3: It is possibly the least likely format to cause confusion and wrongful assumptions

<br>

### Formal specification, as a list of details:

- 1: If a string in this specification is inside single quotes, it is being defined for later use.
- 2: The 'RomVer Format' is defined as "vHUMAN.MAJOR.MINOR", where "HUMAN", "MAJOR", and "MINOR" are each placeholders for positive integers.
- 3: A 'Version' is defined as an ASCII string that follows the RomVer Format, even if the leading "v" is omitted.
- 4: If a 'Project' wishes to follow the RomVer standard, it must follow every following rule.
- 5: Each release of the Project must have exactly one Version attached.
- 6: The contents (counted recursively) of each release of the Project must remain strictly unchanged in every possible manner once released, as much as relavent systems will allow. If the contents of a release require change, the change must be issued as a new release.
- 7: The Version for the first release of the Project must be "v0.1.0" if the project is considered unfit for stable use, or "v1.0.0" if it is considered fit for stable use.
- 8: Each Version of each release (or the New Release) of the Project must be based off the Version of whichever release the New Release was based on (or the Old Release), and must differ according to these rules:
- - If the New Release is considered significantly different in a conceptual sense compared to the Old Release, or if the New Release is considered fit for stable use and the Old Release is not, the HUMAN segment of the Version must be incremented and the MAJOR and MINOR segments must be reset to 0.
- - Otherwise, if users might encounter breaking changes compared to the Old Release, the MAJOR segment of the Version must be incremented and the MINOR segment must be reset to 0, but the HUMAN segment must stay the same.
- - Otherwise, the MINOR segment must be incremented, but the HUMAN and MAJOR segments must stay the same.

<br>

### Specification Extensions

- 9: The RomVer Format may be extended in the following way(s):
- - If a release is a preview for a 'Planned Future Release', its Version must be the expected Version of the Planned Future Release concatenated with "-pre" and a number which is incremented for each preview release for the Planned Future Release and starts at 1.

<br>

This document is inspired by and adapted from [the official specification](https://github.com/romversioning/romver)