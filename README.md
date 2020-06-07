From Ze'ev Atlas and contains a port of the PCRE2 (Perl-Compatible
Regular Expressions) product to z/OS, a later release of PCRE.

  - - - - - - - - - - - - - - - - - - - - - - - - - - - -
  NOTE: This Git Repository was created and managed by
        ZIGI (the z/OS ISPF Git Interface. It is strongly
        suggested that before installing thie repository
        that you install ZIGI from
        https://github.com/wizardofzos/zigi
  - - - - - - - - - - - - - - - - - - - - - - - - - - - -

     (This note pertains to PCRE release 10.35)

     Please see the documents:
     EBCDIC_Horror.txt    member $EBCDIC
     REXXAPI.txt          member REXXAPI

  - - - - - - - - - - - - - - - - - - - - - - - - - - - -

      If you are using code-page 1047 (common in the U.S.), a quick
      install is being presented here, in the form of 6 XMIT-format
      files.  These need to be RECEIVE'd under TSO, and they will be
      almost ready to go.  You still need to read the documentation on
      the PC (and the member PCRE2DOC).

      It is very important to read below, which will explain what to do
      if you need other code pages.

      Port is of PCRE Version 10.35, known as PCRE2.

      Current release is marked with ISPF statistics as 10.35.

      email:  zatlas1@yahoo.com

      web site:  http://www.zaconsultants.net

      PCRE info:  http://www.pcre.org  (please go there)

=======================================================================

Short description:
----- -----------
Regular Expressions is a technology that allows text
search and manipulation in ways that go above and
beyond what is known even to extreme Rexx programmers.
The lack of Regular Expressions in COBOL contrasts with
their availability in Perl and Java and is always
frustrating to me.  Thus, I decided to port a Regular
Expressions library and make it available on native
z/OS.  I chose the pcre2 which is considered to be the
best publicly available such library in that it is
compatible with the standard bearer, Perl.  pcre2 is
used in PHP and other projects.

This is the fifteenth version and is compatible with
pcre2 10.35. The package is distributed as Open Source,
as is with no warranty and under the BSD license that
is pretty open and non-limiting.

=======================================================================

Clarification for other EBCDIC code pages

As per Sam's request, I'll try to clarify the code page issue a
bit farther.  There are two, related but not totally connected
issues.

1. IBM set their C compiler to work with IBM1047, however all the
   machines that I have access to seem to be set to IBM1140 which
   is the old '037' code page.  I had to do some acrobatics and
   replace the caret sign with the IBM logical not (which is the
   caret in IBM1047) for the thing to work.

2. Other languages' EBCDIC code pages issue.

2.1. Originally, I thought to set some switch in the config.h
   header file, in order to allow some logic for various
   languages and code pages.  This was proven to be unnecessary,
   but I did not remove the switches from the header in case I
   will need them sometime in the future.  You should ignore
   those switches.

2.2. OTH, since the only machines that I have access to are in
   the USA, I could not compile or test other languages.  Therefore,
   the supplied LOADLIB is for USA English.  If you want to work
   with other languages like Russian, Hebrew or Turkish, you must
   compile your own version of the LOADLIB.

The good news is that if you run the COMPCRE2 member in the
JCLLIB and all is compiled and bound with RC=4 or less, then you
are good.  The first step builds the correct character table for
your machine and the second step compiles it.

The bad news is that if your caret is in the other place, you
will have to transform it all over the place, especially in the
SRCE and TESTLIB libraries.

Note that there is one line in the source code, in the PCRZOSCS
header file that is marked with '<tag>'.  The caret sign in that
line must stay as caret in the source code.

Ze'ev Atlas


