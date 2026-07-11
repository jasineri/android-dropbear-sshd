# Android Dropbear Builds (Magisk Early-Boot Fork)

=======================

This project is a modified fork based on the original  
[ribbons/android-dropbear](https://github.com/ribbons/android-dropbear) project.

The purpose of this fork is to provide a standalone Dropbear SSH environment
for Android devices running Magisk, designed for very strict and controlled
environments where all required configurations, keys, and runtime data are
located inside one dedicated directory.

The resulting standalone binary is started through Magisk and accepts SSH
connections immediately after boot, even while the phone is still locked and
before the Android user interface has been unlocked.

The main goal is to provide reliable early-boot remote access for advanced
device administration, recovery scenarios, development, testing, and other
controlled environments where access before normal Android startup is required.

---

# Important Security Notice

In order to make Dropbear operate in an early-boot Android environment, some
original security limitations, assumptions, and Android-specific restrictions
have been modified or removed.

These changes were required to make the project work with the intended design,
but they may introduce additional security risks.

The author is not aware of all possible vulnerabilities that could become
possible after these modifications.

By using this software, you acknowledge that:

- The security model differs from the original project.
- The modified environment may expose additional attack surfaces.
- Incorrect configuration may allow unauthorized access.
- The software is provided without any guarantee of security or suitability.
- The author is not responsible for any damage, data loss, device compromise,
  unauthorized access, or other consequences resulting from the use of this
  software.

Use this software only on devices where you understand the risks and have full
control over the environment.

---

# Android Dropbear Builds

![Build status](https://github.com/ribbons/android-dropbear/workflows/Build/badge.svg)

Build scripts and configuration for cross-compiling
[Dropbear](https://matt.ucc.asn.au/dropbear/dropbear.html) for Android.

This fork keeps the original build approach while adapting the output for a
Magisk-based early boot SSH service.

The produced binaries are standalone and designed to run independently from
the Android application environment.

---

# Features

- Standalone Dropbear SSH server binary for Android.
- Starts automatically through Magisk during device boot.
- SSH access available immediately after boot.
- Works while the phone is still locked.
- Does not require Android user unlock before accepting connections.
- All configuration files are stored in one dedicated directory.
- Suitable for controlled recovery and administration environments.
- Supports multiple Android architectures.

---

# Configuration Design

A major design goal of this fork is keeping the complete Dropbear environment
inside one accessible directory.

This directory contains all required files, including:

- Dropbear host keys.
- Authentication configuration.
- Startup configuration.
- Runtime files.
- Additional environment-specific settings.

Keeping everything together allows the SSH service to remain available during
early boot, including situations where normal Android user storage is not yet
available.

The exact directory location depends on the Magisk installation and the device
configuration.

---

# Early Boot Operation

The service is started by Magisk during the boot process.

The expected behavior is:

1. Android device starts.
2. Magisk executes the Dropbear startup script.
3. Dropbear loads configuration from the dedicated directory.
4. SSH becomes available.
5. The device can be accessed remotely before Android unlock.

This behavior is intended for special-purpose administration and recovery
scenarios.

---

# Precompiled Binaries

Precompiled Android binaries may be available as release assets.

Supported architectures include:

- armv7a
- aarch64
- i686
- x86_64

---

# Manual Build

Requirements:

- Android NDK installed at:

```text
$ANDROID_NDK_HOME
````

or:

```text
$ANDROID_HOME/ndk-bundle
```

Build using:

```sh
./build
```

---

# Example Usage

The generated Dropbear binary can be started directly from a Magisk startup
script or another controlled boot environment.

Example:

```sh
dropbear -R -E -p 22
```

The exact command line options depend on the intended security configuration
and device requirements.

---

# Original Project

The original project provides Dropbear builds for Android and the initial
cross-compilation framework.

This fork modifies the original project for:

* Magisk integration.
* Early boot SSH availability.
* Operation before Android unlock.
* Single-directory configuration management.
* Standalone binary deployment.
* More permissive operation required for the intended environment.

---

# License

The majority of code is written by Matt Johnston, under the license below.

Portions of the client-mode work are (c) 2004 Mihnea Stoenescu, under the
same license:

Copyright (c) 2002-2020 Matt Johnston
Portions copyright (c) 2004 Mihnea Stoenescu
All rights reserved.

Additional modifications, build changes, Android/Magisk integration, and fork
specific work are copyright:

Copyright © 2020-2021 Matt Robinson
Copyright © 2026 Nerijus Jasinskas

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


=====

LibTomCrypt and LibTomMath are written by Tom St Denis and others, see
libtomcrypt/LICENSE and libtommath/LICENSE.


=====

sshpty.c is taken from OpenSSH 3.5p1,

Copyright (c) 1995 Tatu Ylonen <ylo@cs.hut.fi>, Espoo, Finland
All rights reserved.

"As far as I am concerned, the code I have written for this software
can be used freely for any purpose. Any derived versions of this
software must be clearly marked as such, and if the derived work is
incompatible with the protocol description in the RFC file, it must be
called by a name other than "ssh" or "Secure Shell"."


=====

loginrec.c
loginrec.h
atomicio.h
atomicio.c
and strlcat() (included in util.c) are from OpenSSH 3.6.1p2, and are licensed
under the 2 point BSD license.

loginrec is written primarily by Andre Lucas, atomicio.c by Theo de Raadt.

strlcat() is (c) Todd C. Miller.


=====

Import code in keyimport.c is modified from PuTTY's import.c, licensed as
follows:

PuTTY is copyright 1997-2003 Simon Tatham.

Portions copyright Robert de Bath, Joris van Rantwijk, Delian
Delchev, Andreas Schultz, Jeroen Massar, Wez Furlong, Nicolas Barry,
Justin Bradford, and CORE SDI S.A.

Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation files
(the "Software"), to deal in the Software without restriction,
including without limitation the rights to use, copy, modify, merge,
publish, distribute, sublicense, and/or sell copies of the Software,
and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE COPYRIGHT HOLDERS BE LIABLE
FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


=====

curve25519.c:

Modified TweetNaCl version 20140427, a self-contained public-domain C library.

https://tweetnacl.cr.yp.to/

Contributors (alphabetical order):

Daniel J. Bernstein, University of Illinois at Chicago and Technische
Universiteit Eindhoven

Bernard van Gastel, Radboud Universiteit Nijmegen

Wesley Janssen, Radboud Universiteit Nijmegen

Tanja Lange, Technische Universiteit Eindhoven

Peter Schwabe, Radboud Universiteit Nijmegen

Sjaak Smetsers, Radboud Universiteit Nijmegen


Acknowledgments:

This work was supported by the U.S. National Science Foundation under grant
1018836. "Any opinions, findings, and conclusions or recommendations expressed
         in this material are those of the author(s) and do not necessarily reflect the
         views of the National Science Foundation."

This work was supported by the Netherlands Organisation for Scientific
Research (NWO) under grant 639.073.005 and Veni 2013 project 13114.

```
```