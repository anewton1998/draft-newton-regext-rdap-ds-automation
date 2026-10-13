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
number: 00
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

This document describes the best current practices for the publication of events
regarding Delegation Signer (DS) records in RDAP domain registrations as described
in RFC10026.

--- middle

# Introduction {#intro}

{{RFC10026}} is a BCP regarding operational practices around the automation of maintenance
of Delegation Signer (DS) DNSSEC resource records. This document describes how that information
should be published in RDAP.

# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations {#security}

TODO Security


# IANA Considerations {#iana}

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

Gavin Brown helped outline the premise of this document.
