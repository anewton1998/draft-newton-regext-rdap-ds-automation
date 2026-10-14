---
###
# Internet-Draft Markdown Template
#
# Rename this file from draft-todo-yourname-protocol.md to get started.
# Draft name format is "draft-<yourname>-<workgroup>-<name>.md".
#
# For initial setup, you only need to edit the first block of fields.
# Only "title" needs to be changed; delete "abbrev" if your title is short.
# Any other content can be edited, but be careful not to introduce errors.
# Some fields will be set automatically during setup if they are unchanged.
#
# Don't include "-00" or "-latest" in the filename.
# Labels in the form draft-<yourname>-<workgroup>-<name>-latest are used by
# the tools to refer to the current version; see "docname" for example.
#
# This template uses kramdown-rfc: https://github.com/cabo/kramdown-rfc
# You can replace the entire file if you prefer a different format.
# Change the file extension to match the format (.xml for XML, etc...)
#
###
title: "Best Current Practices for Publication of DS Automation Events in RDAP"
abbrev: "rdap-ds-auto"
category: bcp

docname: draft-newton-regext-rdap-ds-automation
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number: 
date: 13 October 2026
consensus: true
v: 3
area: OPS
workgroup: REGEXT
keyword:
 - RDAP
 - DNSSEC
venue:
  group: REGEXT
  type: Working Group
  mail: regext@ietf.org
  arch: https://mailarchive.ietf.org/arch/browse/regext/
  github: anewton1998/draft-ietf-newton-rdap-ds-automation
  latest: https://anewton1998.github.io/draft-newton-regext-rdap-ds-automation/

author:
 -
    fullname: Andrew Newton
    organization: ICANN
    email: andy@hxr.us

normative:

informative:

...

--- abstract

This document describes the best current practices for the publication of RDAP events
in domain registrations regarding the automated maintenance of Delegation Signer (DS) records as described
in RFC10026.

--- middle

# Introduction {#intro}

{{!RFC10026}} describes best current practices regarding the automated maintenance
of Delegation Signer (DS) DNSSEC resource records. This document describes the publication
of those maintenance events in RDAP.

{{!RFC9083}} defines an RDAP event as a JSON object with three members, "eventAction", "eventDate", and "eventActor".

{: #event_example title="Example RDAP Event"}
~~~ json
{
  "eventAction": "this thing happened",
  "eventDate": "2026-08-14T00:00:00Z",
  "eventActor": "I did it"
}
~~~

Both the "dsData" and "keyData" structures of the "secureDNS" object in RDAP domain
registrations have distinct events.

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
          "eventAction" : "registration",
          "eventDate" : "2018-03-27T20:09:08Z"
        },
        {
          "eventAction" : "last changed",
          "eventDate" : "2022-04-27T20:19:46Z"
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

# The "DNSSEC Automation" Event Actor

For any event in the "dsData" or "keyData" objects that is a result of an action
taken by the authority of the DNS system (i.e., a domain registry for domains or RIR for reverse-domains, "Registry-Led"),
the "eventActor" MUST have a value of "DNSSEC Automation".

# Event Actions

Use the following registered event actions:

* registration
* last changed
* deletion

RFC10026 mentions historical data... let's discuss.

# "dsAutomation0" RDAP Profile Extension

RDAP servers compliant with this document MUST use the "dsAutomation0" RDAP profile extension,
where profiles are described in {{!I-D.draft-ietf-regext-rdap-extensions}}.

# Security Considerations {#security}

TODO Security


# IANA Considerations {#iana}

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

Gavin Brown helped outline the premise of this document.
