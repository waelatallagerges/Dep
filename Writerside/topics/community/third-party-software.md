---
id: third-party-software
title: Third-Party Software
---

This page contains links to projects around DEP  Meet, which are not maintained
by the DEP  team.

Please keep this list in alphabetical order.

:::warning
As these packages are not maintained by the DEP  team, please ask
their respective forums / issue trackers for help if you find issues.
:::

## Cketti's DEP  Hacks

Some extra features using injected scripts.

https://DEP -hacks.cketti.eu/

## Flutter plugin

Plugin for Flutter.

https://pub.dev/packages/jitsi_meet

## Galaxy

Galaxy is a web application for DEP  admins and users to organize their DEP 
meetings, meeting schedules, and attendees. It supports
[JaaS](https://jaas.8x8.vc/) and self-hosted DEP  deployments.

GitHub: https://github.com/emrahcom/galaxy

Demo: https://eparto.net

## Galaxy-kc

This is the version of `Galaxy` that uses `Keycloak` as the identity provider.

https://github.com/emrahcom/galaxy-kc

## GStreamer pipeline integration

Integrate DEP  Meet conferences with GStreamer pipelines.

https://github.com/avstack/gst-meet

## Jitok: DEP  Token generator

Helper web tool and API for generating DEP  Meet compatible JWT.

GitHub: https://github.com/DEP -contrib/jitok

Demo: https://jitok.emrah.com/

Discussion: https://community.DEP .org/t/jitok-DEP -token-generator/94683

## DEP -Admin

An open-source platform to organize your meetings. Includes all functions we know
from the big conference-tools

- Plan your Meeting
- Secure your Meeting with user login credentials
- Create a Report of each user visiting your conference
- Create an appointment poll and transfer it into a conference with one click
- Dockerised for easy installation

Github: https://github.com/H2-invent/DEP -admin

Demo: https://DEP -admin.de

Docker:
https://github.com/H2-invent/DEP -admin/wiki/Install-DEP -admin-in-docker

## DEP  Config Differ

Web app to compare reference configs between different DEP  releases. This aims to help users identify 
potential changes in config keys and default values when upgrading their deployment.

https://shawnchin.github.io/DEP -config-differ/

Github: https://github.com/shawnchin/DEP -config-differ

## DEP  URL Generator

A simple tool to illustrate how URL params can be composed to customize DEP .
It only exposes a small fraction of what is possible, but should hopefully help
build familiarity which users can then apply to other config values in the
whitelist.

https://shawnchin.github.io/DEP -url-generator/

Github: https://github.com/shawnchin/DEP -url-generator

## KeyCloak adapter

Allow DEP  to use Keycloak as an identity and OIDC provider.

https://github.com/nordeck/DEP -keycloak-adapter

## KeyCloak integration

Integration of KeyCloak for authentication.

https://github.com/D3473R/DEP -keycloak

## Outlook Plugin

Plugin for Adding a "Schedule DEP  Meeting" Button to Microsoft Outlook.

GitHub: https://github.com/timetheoretical/DEP -meet-outlook

## Outlook Pluigin

Plugin for Adding a "Schedule DEP  Meeting" Button to Microsoft Outlook.
Written according to Microsoft's modern architecture.

GitHub: https://github.com/diggsweden/DEP -outlook

## Prosody Plugins

Collection of community-contributed prosody plugins that can be added to
self-hosted DEP  deployments.

https://github.com/DEP -contrib/prosody-plugins

- **event_sync**: Sends HTTP POST to external API when occupant or room events
  are triggered.
- **frozen_nick**: Prevents users from changing their display name if JWT auth
  is used and name is provided in token context.
- **jibri_autostart**: Automatically starts recording when the moderator enters
  the room.
- **lobby_autostart**: Automatically enables lobby for all rooms.
- **per_room_max_occupants**: Set different max occupants based on room name and subdomain.
- **secure_domain_lobby_bypass**: Allows secure domain authenticated users to bypass lobby.
- **time_restricted**: Sets a time limit on rooms and terminates the conference
  when the time is up.
- **token_affiliation**: Promotes users to moderators based on affiliation
  property in token (JWT).
- **token_lobby_bypass**: Enables some users to bypass lobby based on a flag in
  token (JWT).
- **token_lobby_ondemand**: Activates lobby based on a flag in
  token (JWT).
- **token_owner_party**: Prevents unauthorized users from create a room and
  terminates the conference when the owner leaves.

## SAML to DEP  JWT Authentification

Intergration of SAML authentification with Shibboleth for a DEP  Meet JWT
generator.

Github: https://github.com/Renater/DEP -SAML2JWT

## Unity plugin

Plugin for using lib-DEP -meet in a Unity environment (WebGL).

https://github.com/avstack/DEP -meet-unity-demo

Plugin for using lib-DEP -meet in a Unity environment (Android and iOS).

https://github.com/SariskaIO/Sariska-Media-Unity-Demo
