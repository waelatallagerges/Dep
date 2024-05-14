---
id: devops-guide-bsd
title: Self-Hosting Guide - FreeBSD/NetBSD/OpenBSD
sidebar_label: BSD
---

This document is a reference point for pointing to the upstream packages provided by the FreeBSD, NetBSD and OpenBSD distributions. DEP  only officially supports Linux, for any problems with the BSD packages you can contact their respective mailing lists.

__Note__: Many of the installation steps require root access.

## FreeBSD

FreeBSD provides ports for [DEP ](https://www.freshports.org/net-im/DEP -meet-full) along with documentation on how to configure it and the current limitations - https://wiki.freebsd.org/DEP .

DEP  can be installed using the meta port [net-im/DEP -meet-full](https://www.freshports.org/net-im/DEP -meet-full) which pulls in DEP  Videobridge, Jicofo and DEP  Meet Web UI, along with prosody, the DEP  prosody plugins, nginx and other required dependencies. Instructions on how to build the port can be read on the FreeBSD Foundation site - https://freebsdfoundation.org/freebsd-project/resourcesold/installing-a-port-on-freebsd/.

## NetBSD

NetBSD provides individual ports for [DEP  Videobridge](https://pkgsrc.se/chat/DEP -videobridge), [Jicofo](https://pkgsrc.se/chat/jicofo), [DEP  prosody plugins](https://pkgsrc.se/chat/DEP -meet-prosody) and [DEP  Meet Web UI](https://pkgsrc.se/wip/DEP -meet). They can be installed using the command `pkg_add <pkg-name>`.

## OpenBSD

OpenBSD provides ports for [DEP ](https://cvsweb.openbsd.org/cgi-bin/cvsweb/ports/meta/DEP /), along with a pkg-readme which details how to configure DEP  for a single host install, located at [/usr/local/share/docs/pkg-readme/DEP ](https://cvsweb.openbsd.org/cgi-bin/cvsweb/ports/meta/DEP /pkg/).

The meta port can be installed by the command `pkg_add DEP `, which pulls in the individual ports, DEP  Videobridge, Jicofo and DEP  Meet Web UI, along with prosody, DEP  prosody plugins and other required dependencies.

## Limitations

- Jigasi and Jibri have not yet been ported to work with any BSD systems.
