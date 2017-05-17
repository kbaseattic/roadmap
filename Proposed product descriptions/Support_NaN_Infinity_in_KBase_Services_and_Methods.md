# Support Nan and Inf in KBase services

##Summary:

The clients, services, and methods produced by the KIDL type compiler and the
SDK transport data from client to server and vice versa in
[JavaScript Object Notation](http://json.org/) (JSON). JSON is simple and
human-readable, but lacks support for representing the values Not a Number
(NaN) and positive and negative infinity (+/-Infinity). Update the SDK to
produce services that support NaN and +/-Infinity (NaInf).

##Story/Description:

Currently all typecompiler or SDK generated KBase services and methods
transport data in JSON format. Thus, any object / data to be
sent to a KBase service (including the Workspace service for storage) must be
representable as JSON. The most glaring omission in the JSON specification,
from the point of view of a scientist, is the lack of support for NaN and
Infinity. These values frequently occur in scientific data to indicate missing
or invalid data or values that are outside the measurable range of an
experiment or instrument.

To support NaInf, extend the server and client code in all
supported languages to read and emit JSON containing barewords that represent
the three values. [Preliminary work](https://github.com/MrCreosote/TalkJSONToMe)
shows that:

* The Python json standard library package, by default, emits and consumes the
  barewords NaN and +/-Infinity. Alternate barewords are not configurable.
* The Java Jackson JSON library can be configured to emit and consume NaN and
  +/-Infinity. Alternate barewords are not configurable.
* Javascript can be altered to emit and consume NaN and +/-Infinity with some
  additional code. However, this means browser built in JSON parsers cannot be
  used. Additionally, since NaN and Infinity are object properties rather than
  literals, care needs to be taken in the implementation.
* Perl's JSON module emits nan and +/-inf barewords rather than NaN and
  +/-Infinity. It cannot parse NaN and +/-Infinity barewords. Based on a
  cursory examination of the code, it appears the underlying C library may
  need changes in order to be compatible with the other languages.
  
##Approach:

Python and Java support is trivial and needs no further work other than minor
client and server updates. Engage KBase language experts for Perl, JavaScript,
and R to properly implement NaInf support in the SDK clients and
servers.

##User stories:
Bench biologists and 3rd party developers see that NaN and Infinity may be
represented in KBase object data and used as input to KBase SDK methods.

A user would like to upload and use a collection of RNAseq gene expression
ratios as a FeatureValue matrix. Some of the genes were never observed in only
certain samples, hence when creating comparisons between treatment and control
samples those sample values and sample-to-sample ratios need to allow an NaN
value corresponding to 'gene was not measured'. This is to distinguish from 0
values which would correspond to a actual measurement, would be included in
normalization etc.

##Narrative Mockup:

N/A

##Timeline:

1 sprint.

##Test Plan:

Add tests to the kb_sdk module as appropriate to ensure the various languages
can exchange NaInf.

##Citations:

N/A
