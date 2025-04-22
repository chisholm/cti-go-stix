# README

## OASIS TC Open Repository: cti-go-stix

This GitHub public repository [cti-go-stix](https://github.com/oasis-open/<cti-go-stix>/) was created at the request of the [CTI TC](https://groups.oasis-open.org/communities/tc-community-home2?CommunityKey=c6c33da0-d1ee-42dd-9427-018dc7d32277) as an [OASIS TC Open Repository](https://www.oasis-open.org/resources/open-repositories/) to support development of open source resources related to Technical Committee work.

While this TC Open Repository remains associated with the sponsor TC, its development priorities, leadership, intellectual property terms, participation rules, and other matters of governance are [separate and distinct](https://github.com/oasis-open/cti-go-stix/blob/master/CONTRIBUTING.md) from the OASIS TC Process and related policies.

All contributions made to this TC Open Repository are subject to open source license terms expressed in the [BSD-3-Clause License](https://opensource.org/licenses/BSD-3-Clause). That license was selected as the declared [applicable license](https://www.oasis-open.org/resources/open-repositories/licenses) when the TC Open Repository was created.

As documented in [CONTRIBUTING](https://github.com/oasis-open/cti-go-stix/blob/master/CONTRIBUTING.md), contributions to this OASIS TC Open Repository are invited from all parties, whether affiliated with OASIS or not. Participants must have a GitHub account, but no fees or OASIS membership obligations are required. Participation is expected to be consistent with the [OASIS TC Open Repository Guidelines and Procedures](https://www.oasis-open.org/policies-guidelines/open-repositories), the open source [LICENSE](https://github.com/oasis-open/cti-go-stix/blob/master/LICENSE) designated for this particular repository, and the requirement for an [Individual Contributor License Agreement](https://www.oasis-open.org/resources/open-repositories/cla/individual-cla) that governs intellectual property.

## Statement of Purpose

OASIS Go STIX API: a repository containing the MVP implementation of Go STIX APIs

## Simple Usage

A STIX object is a Go map.  The Go type is named `STIXObject` and is based
on a `map[string]any`.  To invoke validation from another map, one can call
`STIXObject.FromMap()`:

```go
var indicator STIXObject
err := indicator.FromMap(map[string]any{
    "type": "indicator",
    "name": "File hash for malware variant",
    "indicator_types": []any{"malicious-activity"},
    "pattern_type": "stix",
    "pattern": "[file:hashes.md5 = 'd41d8cd98f00b204e9800998ecf8427e']",
    "valid_from": "2014-08-25T15:00:07.527004Z",
})
```

This will populate the `indicator` map with validated/cleaned content from
the given map data.  There are some STIX object initialization conveniences,
for example a STIX ID is created automatically with a UUIDv4 (or a
deterministic ID for SCOs with ID contributing properties), and versioning
properties are added in objects of versionable types, with the current
timestamp.  So it is okay to omit them in the map above.

Creating a `STIXObject` from JSON will automatically invoke
cleaning/validation:

```go
// assuming import "encoding/json"
var indicator STIXObject
err := json.Unmarshal([]byte(
    `{
        "type": "indicator",
        "spec_version": "2.1",
        "id": "indicator--dbcbd659-c927-4f9a-994f-0a2632274394",
        "created": "2017-09-26T23:33:39.829Z",
        "modified": "2017-09-26T23:33:39.829Z",
        "name": "File hash for malware variant",
        "indicator_types": [
            "malicious-activity"
        ],
        "pattern_type": "stix",
        "pattern_version": "2.1",
        "pattern": "[file:hashes.md5 ='d41d8cd98f00b204e9800998ecf8427e']",
        "valid_from": "2017-09-26T23:33:39.829952Z"
    }`,
), &indicator)
```

Being a map, the Go standard library already knows how to serialize a
`STIXObject` to a JSON object.  Instances of special types which the
cleaning process puts into the map have custom JSON serialization included
with this library.  So one can dump to JSON using standard APIs as usual:

```go
// assuming import "encoding/json"
jsonBytes, err := json.Marshal(indicator)
```

### Extensions and Custom Content

STIX 2.0 style "custom" content is not supported.  This means that it is
not possible to add arbitrary custom top-level properties to a registered
object type, in the absence of a toplevel property extension.  Additional
2.0 style markings can't be registered (tlp 1.0 and statement markings are
supported).  Unregistered subtype extensions will cause an error.

STIX 2.1 style extensions are supported, however.  Unregistered extension
objects are passed through without error, with the exception that
spec-defined common properties are still checked (e.g. version timestamps,
STIX ID, etc).  Unregistered property extensions allow arbitrary properties.


## <a id="maintainers">Maintainers</a>

TC Open Repository [Maintainers](https://www.oasis-open.org/resources/open-repositories/maintainers-guide) are responsible for oversight of this project's community development activities, including evaluation of GitHub [pull requests](https://github.com/oasis-open/<repoName>/blob/master/CONTRIBUTING.md#fork-and-pull-collaboration-model) and [preserving](https://www.oasis-open.org/policies-guidelines/open-repositories#repositoryManagement) open source principles of openness and fairness. Maintainers are recognized and trusted experts who serve to implement community goals and consensus design preferences.

Initially, the TC members have designated one or more persons to serve as Maintainer(s); subsequently, participating community members may select additional or substitute Maintainers, by [consensus agreements](https://www.oasis-open.org/resources/open-repositories/maintainers-guide#additionalMaintainers). 

<a id="currentMaintainers">Current Maintainers</a> of this TC Open Repository are: 

- [Rich Piazza](rpiazza@mitre.org), [rpiazza](https://github.com/rpiazza), [MITRE](https://www.mitre.org/) 
- [Marlon Taylor](Marlon.Taylor@mail.cisa.dhs.gov), GHID, [DHS CISA](https://www.cisa.gov/)

## About OASIS TC Open Repositories

- [TC Open Repositories: Overview and Resources](https://www.oasis-open.org/resources/open-repositories/)

- [Frequently Asked Questions](https://www.oasis-open.org/faq-tc-repo/)

- [Open Source Licenses](https://www.oasis-open.org/resources/open-repositories/licenses)

- [Contributor License Agreements (CLAs)](https://www.oasis-open.org/policies-guidelines/open-projects-process/#CLAs-license-notices)

- [Maintainers' Guidelines and Agreement](https://www.oasis-open.org/resources/open-repositories/maintainers-guide)

## Feedback

Questions or comments about this TC Open Repository's activities should be composed as GitHub issues or comments. If use of an issue/comment is not possible or appropriate, questions may be directed by email to the Maintainer(s) listed above. 

Please send general questions about TC Open Repository participation to OASIS Staff at repository-admin@oasis-open.org and any specific CLA-related questions to repository-cla@oasis-open.org.
