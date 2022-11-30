# Finger Request

## Preamble

The **finger-protocol** is a simple, friendly, human-oriented & human-legible protocol, that has its origins in the early 1970s.

Although some of the usage of the **finger-protocol** was similar to a directory-service for humans — it evolved into one of the early Internet-based social networks.
It was not uncommon for people to publish personal information, contact information, referencs to that person's presence on other parts of the Internet, a short biography, a journal, articles, jokes, (so called) ASCII art, and more, via the **finger-protocol**.

One should note that online social networks existed on other pre-Internet networks.
So, while the **finger-protocol** wasn't the first online social network — it is important because of just how important the Internet became.

The **finger-protocol** was created and evolved over time, by the software developers who created the **finger-client** software, and the **finger-server** software.
Later on — at least 6 years after the **finger-protocol** was first created, IETF RFC-742 was published, in an attempt to describe the pre-existing **finger-protocol**.
I.e., IETF RDC-742 did _not_ create a new protocol, but instead just tried to document what was created by software developers outside of the IETF.
14 years later after RFC-742 was published, and at least 20 years after the **finger-protocol** first existed and was evolving — RFC-1288 was published in an attempt to remove some of (what some perceived as) the ambiguity of RFC-742, to make it easier for both people who would implement a **finger-protocol** client or server, and to provide some guidance.
However RFC-1288 added restrictions to the **finger-protocol** that did NOT exist in RFC-742.
In 1991 some of these restrictions may have seemed reasonable, however today (in 2022) some of the restrictions probably do not make as much sense (and should probably be reconsidered). This document is in part an attempt to reconsider one of these restrictions that RFC-1288 introduced but which didn't exist in RFC-742.

## Introduction

This document is an updated specification for a **finger-protocol** request

## Finger-Query Specification

Using the same style of notation as IETF RFC-1288, here is an updated specification for a **finger-query**:
```
        {Q1}    ::= [{W}|{W}{S}{U}]{C}

        {Q2}    ::= [{W}{S}][{U}]{H}{C}

        {U}     ::= username

        {H}     ::= @hostname | @hostname{H}

        {W}     ::= /switchname

        {S}     ::= <SP> | <SP>{S}

        {C}     ::= <CRLF>
```

## What Changed

The change is the definition of `{W}`.

In IETF RFC-1288 it was:
```
        {W}     ::= /W
```

In this document, it has been updated to:
```
        {W}     ::= /switchname
```

What this means is that — instead of the **finger-protocol** just having this switch:
```
/W
```

The **finger-protocol**  can have any of these types of switches too:
```
/PUSH
/PULL
/LIST
/PICK
/banana
/path/to/something.ext
/once
/once/twice
/once/twice/thrice
/once/twice/thrice/fource
```
