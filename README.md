ruby-openksi
============

Ruby interface to the OpenKSI (Keyless Signature Infrastructure) digital
signature/time stamping protocol. Defaults to use the free Guardtime KSI
service.

## Purpose

The goal of this project is to provide a pure Ruby interface to the
OpenKSI API. The software defaults to use the free (non-commercial)
offering provided by [Guardtime](http://www.guardtime.com) but can be
configured to use an arbitrary KSI provider.

KSI can be used to provably verify that a given string (or entire
document) existed at a specific point in time and has not been modified
since that moment.

## NOT IMPLEMENTED (yet)

In the spirit of Readme Driven Development I've captured a lot of
documentation here before beginning to code. Through this research I've
found that there is quite a lot of prework that must be done before we
can have a pure-Ruby implementation of KSI.

Specifically:

* Ability to encode/decode ASN.1 data. _Done. This is a part of the
  Ruby stdlib._
* Ability to parse Cryptographic Message Syntax (CMS), i.e., implement
  [RFC 2630](https://www.ietf.org/rfc/rfc3370.txt).
* Ability to represent [RFC 3161](https://www.ietf.org/rfc/rfc3161.txt)
  x.509 Public Key Infrastructure Time Stamp Protocol (PKI TSP).

IMO, RFC 2630 and RFC 3161 libraries should stand alone as separate
projects that would become dependencies of this one.

For the time being this project is larger than what I'm able to do in my
spare time, but I'm leaving this documentation in place. If you end up
implementing KSI or either of the dependencies listed above please
advise so that I may update these docs to point people in the right
direction.

_In the meantime_, you may be interested in:
[ristik/ruby-guardtime](https://github.com/ristik/ruby-guardtime). It is
a Ruby implementation of a Guardtime interface, but written as a wrapper
to a C extension instead of pure Ruby.

## Usage

There are two steps to using KSI: signing and verifying.

In the signing phase you provide a hash of your string to the library,
that will send your hash to the Guardtime service and return an
RFC3161-compliant reponse.

To verify a string, you provide the KSI hash and your original document
hash. The Guardtime service will respond with verification information.

## About Keyless Signature Infrastructure

Keyless Signature Infrastructure (KSI) is a web-scale digital
signature/timestamp system for electronic data. The term ‘keyless’
denotes that the signatures can be reliably verified without assuming
secrecy of cryptographic keys. Keyless signatures are not vulnerable to
key compromise implying that their lifetime is based only on the
security properties of the cryptographic hash function and also that
their security properties will survive intact when practical quantum
computing becomes a reality.
(source: [OpenKSI](http://www.openksi.org/refer/))

## About Guardtime

Guardtime is a commercial service that implements the KSI. They provide
a free service for non-commercial use and a for-pay service that can be
used commercially.

In essense, Guardtime adds the hash of your string to a large hash tree
and regularly publishes the root node of that tree in paper-based and
electronic media. This allows you to prove that your string existed at a
specific date and time and has not been modified.

## Reference

* [OpenKSI](http://www.openksi.org)
* [Wikipedia article on Linked
  Timestamping](https://en.wikipedia.org/wiki/Linked_timestamping)
* [rsyslog log
  signatures](http://blog.gerhards.net/2013/05/rsyslogs-first-signature-provider-why.html)
  The `rsyslog` maintainer's blog post on why he chose to use KSI as the
  technology of choice for log verification.
* [ristik/ruby-guardtime](https://github.com/ristik/ruby-guardtime)
  Another Ruby implementation of a Guardtime interface, but written as a
  C extension instead of pure Ruby.
* [KSI Technical Reference – Appendix: Formats and
  Algorithms](http://www.openksi.org/wp-content/uploads/2013/03/KSI-Reference-RFC3161-Formats-and-Algorithms-v1.18.pdf)
* [KSI Technical
  Reference](http://www.openksi.org/refer/ksi-technical-reference/)

