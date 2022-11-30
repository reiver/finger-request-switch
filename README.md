# Finger Request
by [Charles Iliya Krempeaux](http://changelog.ca/)

## Preamble

The **finger-protocol** is a simple, friendly, human-oriented & human-legible protocol, that has its origins in the early 1970s.

Although some of the usage of the **finger-protocol** was similar to a directory-service for humans — it evolved into one of the early Internet-based social networks.
It was not uncommon for people to publish personal information, contact information, referencs to that person's presence on other parts of the Internet, a short biography, a journal, articles, jokes, (so called) ASCII art, and more, via the **finger-protocol**.

One should note that online social networks existed on other pre-Internet networks.
So, while the **finger-protocol** wasn't the first online social network — it is important because of just how important the Internet became.

The **finger-protocol** was created and evolved over time, by the software developers who created the **finger-client** software, and the **finger-server** software (as well as the user who chose to use or not use a particular implementation).
Later on — at least 6 years after the **finger-protocol** was first created, IETF RFC-742 was published, in an attempt to describe the pre-existing **finger-protocol**.
I.e., IETF RDC-742 did _not_ create a new protocol, but instead just tried to document and describe what was created by software developers outside of the IETF.
14 years later after RFC-742 was published, and at least 20 years after the **finger-protocol** first existed and was evolving — RFC-1288 was published in an attempt to remove some of (what some perceived as) the ambiguity of RFC-742, to make it easier for both people who would implement a **finger-protocol** client or server, and to provide some guidance.
However RFC-1288 added restrictions to the **finger-protocol** that did NOT exist in RFC-742.
In 1991 some of these restrictions may have seemed reasonable, however today (in 2022) some of the restrictions probably do not make as much sense (and should probably be reconsidered). This document is in part an attempt to reconsider one of these restrictions that RFC-1288 introduced but which didn't exist in RFC-742 — in particular, how to handle a **switch** other than the `"/W"` switch.

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

## Parsing

Given a **finger-request** —

For example —
```
"/PULL dariush@changelog.ca\r\n"
```

One can tell if a **finger-request** has a **switch** by looking at the first character of the finger-request.

If it is a `"/"` character (i.e., a solidus character), then the **finger-request** has a **switch**.
Else if it isn't a `"/"` character (i.e., a `solidus` character), then the **finger-request** doesn't have a **switch**.

All the characters following the `"/" character` (i.e., the `solidus` character) up to, but not including a `space` character or (if there is not `space` character) a terminaling "\r\n" (i.e., `<CRLF>`), is part of the `switchname`.

So, for example, with out example **finger-request** —
```
"/PULL dariush@changelog.ca\r\n"     
```

The `switchname` is `"PULL".`

## Examples

Here are a number of example **finger-requests** where we specify what the `switchname` is

```
/PUSH
# switchname = "PUSH"

/PULL
# switchname = "PULL"

/LIST
# switchname = "LIST"

/PICK
# switchname = "PICK"

/banana
# switchname = "banana"

/path/to/something.ext
# switchname = "path/to/something.ext"

/once
# switchname = "once"

/once/twice
# switchname = "once/twice"

/once/twice/thrice
# switchname = "once/twice/thrice"

/once/twice/thrice/fource
# switchname = "once/twice/thrice/fource"
```
