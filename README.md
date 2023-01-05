# Darkwolf UID (DWUID) Specification

&copy; 2023 Pavel Wolf <cyberviking@darkwolf.team>

## 1. Abstract

Darkwolf UID (DWUID) — universally unique lexicographic human-friendly decentralized identifier, used to identify any entities or objects in the real world.

## 2. Structure

DWUID is bit sequence consisting of a 4-bit version and an N-bit identifier, where N, depending on the version, can be constant or changeable.

The representation of a 24-bit DWUID consisting of 3 bytes:

`1XXXYYYY YYYYYYYY YYYYYYYY`

X — version bits \
Y — identifier bits

## 3. Versions

At the moment, the specification describes 4 versions of the identifier.

### 3.1. Timestamp

The version of the identifier based on a timestamp since Unix epoch in milliseconds, optionally padded with a unique sequence.

The Timestamp version of the DWUID is a bit sequence consisting of the 4-bit version, the 48-bit timestamp since the Unix epoch in milliseconds, and optionally padded with an N-bit unique sequence.

It is recommended to use a 68-bit unique sequence to get a 120-bit DWUID that will have
constant length, depending on the encoding, 20-21 characters in text representation.

The Timestamp version representation of a 120-bit DWUID consisting of 15 bytes:

`1000XXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXYYYY YYYYYYYY YYYYYYYY YYYYYYYY YYYYYYYY YYYYYYYY YYYYYYYY YYYYYYYY YYYYYYYY`

X — timestamp bits in milliseconds \
Y — unique sequence bits

### 3.2. Random

The version of the identifier based on cryptographically secure random or pseudo-random sequence.

The Random version of the DWUID is a bit sequence consisting of a 4-bit version and an N-bit random sequence.

It is recommended to use a 116-bit random sequence to get a 120-bit DWUID that will have
constant length, depending on the encoding, 20-21 characters in text representation.

The Random version representation of a 120-bit DWUID consisting of 15 bytes:
 
`1001XXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX`

X — random sequence bits

### 3.3. Geohash

The version of the identifier based on geographic latitude and longitude coordinates represented as a one-dimensional space.

The Geohash version of the DWUID is a bit sequence consisting of a 4-bit version and a 56-bit one-dimensional space representation.

Empirically, it was found that a 56-bit representation of one-dimensional space is sufficient to encode using floating point arithmetic geographic coordinates of latitude and longitude with an accuracy of up to 6 decimal places inclusive.

The Geohash version representation of a 60-bit DWUID consisting of 8 bytes:

`1010XXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXXXXXX XXXX0000`

X — one-dimensional space representation bits

### 3.4. Hash

The version of the identifier based on digest obtained using the BLAKE3 hashing algorithm.

In developing.

## 4. Encodings

The encodings used in the DWUID text representation are based on alphabets with lexicographic character order.

### 4.1 Base58

Alphabet symbols:

`123456789ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz`

`I` и `l` — aliases for `1` \
`0` и `O` — aliases for `o`

### 4.2 Base64

Alphabet symbols:

`-0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ_abcdefghijklmnopqrstuvwxyz`