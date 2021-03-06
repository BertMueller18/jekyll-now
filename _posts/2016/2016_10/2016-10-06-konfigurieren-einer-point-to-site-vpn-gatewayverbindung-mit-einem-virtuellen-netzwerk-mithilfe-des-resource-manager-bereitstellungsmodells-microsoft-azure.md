---
layout: post
published: true
title: "Konfigurieren einer Point-to-Site-VPN-Gatewayverbindung mit einem virtuellen Netzwerk mithilfe des Resource Manager-Bereitstellungsmodells | Microsoft Azure"
date: 2016-10-06T07:06:59.136Z
categories: vpn networking azurerm
link: https://azure.microsoft.com/de-de/documentation/articles/vpn-gateway-howto-point-to-site-rm-ps/
tags:
  - links
ogtype: article
bodyclass: post
---

## Konfigurieren einer Point-to-Site-VPN-Verbindung (P2S) mit einem VNet mithilfe von PowerShell

Von Cheryl McGuire
Aktualisiert: 31.08.2016  
In GitHub bearbeiten
Resource Manager – PowerShellKlassisch – Klassisches Portal
Mit einer P2S-Konfiguration (Point-to-Site) können Sie von einem einzelnen Clientcomputer eine sichere Verbindung mit einem virtuellen Netzwerk herstellen. Eine P2S-Verbindung ist nützlich, wenn Sie von einem Remotestandort, z.B. von zu Hause oder in einer Konferenz, eine Verbindung mit Ihrem VNet herstellen möchten. Diese Methode eignet sich auch, wenn Sie nur wenige Clients besitzen, die mit einem virtuellen Netzwerk verbunden werden müssen.

Dieser Artikel führt Sie durch die Erstellung eines VNet mit einer P2S-Verbindung im Resource Manager-Bereitstellungsmodell. Für diese Schritte ist PowerShell erforderlich. Derzeit ist es nicht möglich, diese Lösung komplett über das Azure-Portal zu erstellen.
