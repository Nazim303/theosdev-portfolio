---
layout: ../../../layouts/BlogLayout.astro
title: "CELLTEST POSITIVE: Building an Asymmetric Network Architecture"
date: "2026-07-28"
author: "TheosDev"
pinned: true
summary: "Synchronizing the health pool as a resource unit in Host (Cancer) and Client (Antibody) architecture using Netcode for GameObjects."
---

# Using Player Health as a Resource

One of the biggest challenges while developing the game was completely abandoning the traditional mana system and enabling the player to use their own health (`HP`) as a resource. Here is how I validated this state server-side using Netcode for GameObjects (NGO).

## 1. RPC Calls and Security
When the Client (Antibody player) wants to play a card, they cannot directly subtract from their own health. Instead, they send a `ServerRpc` to the server.

* The server checks whether the player has enough health.
* If health is sufficient, the card spawns on the field.
* Then, the server updates the UI health bars of both players via a `ClientRpc`.

Thanks to this asymmetric setup, we successfully prevented client-side cheating!