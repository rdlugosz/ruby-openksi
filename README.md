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
[_source: [OpenKSI](http://www.openksi.org/refer/)_]

## About Guardtime

Guardtime is a commercial service that implements the KSI. They provide
a free service for non-commercial use and for-pay service that can be
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

