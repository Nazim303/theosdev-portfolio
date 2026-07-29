---
layout: ../../layouts/BlogLayout.astro
title: "Devlog: CELLTEST POSİTİVE için Asimetrik Ağ Mimarisi Kurulumu"
date: "2026-08-15"
author: "TheosDev"
---

# Oyuncu Canını Kaynak Olarak Kullanmak

Oyun geliştirirken en büyük zorluklardan biri, alıştığımız mana sistemini tamamen terk edip, oyuncunun kendi canını (`HP`) kaynak olarak kullanmasını sağlamaktı. Netcode for GameObjects (NGO) kullanarak bu durumu sunucu tarafında nasıl doğruladığımı anlatacağım.

## 1. RPC Çağrıları ve Güvenlik
Client (Antikor oyuncusu), bir kart oynamak istediğinde doğrudan kendi canını düşüremez. Bunun yerine sunucuya bir `ServerRpc` gönderir.

* Sunucu oyuncunun yeterli canı olup olmadığını kontrol eder.
* Eğer can yeterliyse, kart sahaya doğar (Spawn).
* Ardından sunucu bir `ClientRpc` ile her iki oyuncunun UI (Arayüz) barlarını günceller.

Bu asimetrik yapı sayesinde hile yapılmasının önüne geçtik!