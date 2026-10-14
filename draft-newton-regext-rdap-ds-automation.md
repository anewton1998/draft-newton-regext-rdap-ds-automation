---
title: "RDAP Extensions for the Publication of DS Automation Events"
abbrev: "rdap-ds-auto"
category: std

docname: draft-newton-regext-rdap-ds-automation-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date: 14 October 2026
consensus: true
v: 3
area: "Operations and Management"
workgroup: "Registration Protocols Extensions"
keyword:
 - RDAP
 - DNSSEC
venue:
  group: "Registration Protocols Extensions"
  type: "Working Group"
  mail: "regext@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/regext/"
  github: "anewton1998/draft-newton-regext-rdap-ds-automation"
  latest: "https://anewton1998.github.io/draft-newton-regext-rdap-ds-automation/draft-newton-regext-rdap-ds-automation.html"

author:
 -
    fullname: Andrew Newton
    organization: ICANN
    email: andy@hxr.us
 -
    fullname: Jasdip Singh
    organization: ARIN
    email: jasdips@arin.net

normative:

informative:

...

--- abstract

This document describes two RDAP extensions for the publication of RDAP events
in domain registrations regarding the automated maintenance of Delegation Signer (DS) records as described
in RFC10026.

--- middle

# Introduction {#intro}

{{!RFC10026}} describes best current practices regarding the automated maintenance
of Delegation Signer (DS) DNSSEC resource records where multiple parties may have channels
to create and/or update those records. This document describes two RDAP extensions for the publication
of those maintenance events in RDAP which can be used to troubleshoot the multi-party
maintenance of these records.

Both extensions use the RDAP event data structure defined in {{!RFC9083}}, which has three members, "eventAction", "eventDate", and "eventActor".

{: #event_example title="Example RDAP Event"}
~~~ json
{
  "eventAction": "this thing happened",
  "eventDate": "2026-08-14T00:00:00Z",
  "eventActor": "I did it"
}
~~~

Both the "dsData" and "keyData" structures of the "secureDNS" object in RDAP domain
registrations (as defined in {{RFC9083}} have distinct events.

{: #secureDNS_example title="Example RDAP secureDNS object"}
~~~ json
"secureDNS" : {
  "delegationSigned" : true,
  "dsData" : [
    {
      "algorithm" : 13,
      "digest" : "B9BEC0EAC0F064929C8586DB185537787015EC3A48F0894BEA74DEEA452F3060",
      "digestType" : 2,
      "events" : [
        {
          "eventAction" : "an action",
          "eventActor"  : "foo@example.com",
          "eventDate"   : "2018-03-27T20:09:08Z"
        },
        {
          "eventAction" : "another action",
          "eventActor"  : "https://example.com/bar.html",
          "eventDate"   : "2022-04-27T20:19:46Z"
        }
      ],
      "keyTag" : 47828
    }
  ]
}
~~~

The "eventAction" value of RDAP events are registered in the IANA RDAP JSON values
registry.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# DS Automation Events {#ds_automation_events}

## Event Actions

This document defines the following event actions, which are specific to DS automation:

* "ds automation instantiation" - DS automation caused the instantiation of this DNSSEC information
* "ds automation update" - DS automation caused the update of this DNSSEC information
* "ds automation removal" - DS automation caused the removal of this DNSSEC information

## Event Actors

The "eventActor" MUST be either an email address or URL identifying the party attributed to the event.
If an HTTPS URL is given, it should both identify the party attributed to the event and reference
a web page with information describing the operational nature of the event.

# The "dsAutomation0" RDAP Extension

The "dsAutomation0" extension is an RDAP profile,
where an RDAP extension that is a profile is described in {{!I-D.draft-ietf-regext-rdap-extensions}}.
That is, it relies only on the RDAP queries defined in {{!RFC9082}} and data structures
in {{!RFC9083}} and should be interoperable with all existing RDAP clients that support the domain
lookup query.

When responding to domain lookups ({{Section 3.1.3 of RFC9082}}), servers compliant with the
"dsAutomation0" extension MUST describe "dsData" and "keyData" events as described in {{ds_automation_events}}
for the domain registration at it exists in the registration system at the time of query
(i.e., these are not historical events but represent the current state of the registration).
As such, it is not expected that "ds automation removal" would appear in these events.

# The "dsAutomationHistory0" RDAP Extension

The "dsAutomationHistory0" extension defines a query path similar to {{Section 3.1.3 of RFC9082}} and
produces a domain object as defined in {{Section 5.3 of RFC9083}}.

The query path is "dsAutomationHistory0_domain" followed by the \<domain name\> segment
as described in {{Section 3.1.3 of RFC9082}}.

{: #dsAutomationHistory0_query_example title="Example DS Automation History Query"}
~~~
https://rdap.regy.example/dsAutomationHistory0_domain/foo.example
~~~

The resulting domain object MUST contain historical events for "dsData" and "keyData" events
as described {{ds_automation_events}}. The events given MUST include all "dsData" and "keyData"
events since the RDAP server began supporting the "dsAutomationHistory0" extension on a per
domain registration basis (i.e., if foo.example is deleted and re-registered, the server is not
expected to produce events from the first registration of foo.example registration).

# The "ttl0" RDAP Extension

{{!RFC10026}} describes the use of the "ttl0" RDAP extension described in {{!RFC10037}}.
Use of the "ttl0" extension with the "dsAutomation0" and "dsAutomationHistory0" results
is also recommended.

# Security Considerations {#security}

TODO Security


# IANA Considerations {#iana}

TODO register "dsAutomation0"

TODO register "dsAutomationHistor0"

TODO register "ds automation instantiation"

TODO register "ds automation update"

TODO register "ds automation removal"

--- back

# Acknowledgments
{:numbered="false"}

Gavin Brown helped outline the premise of this document.
