# Projekt: Implementierung einer segmentierten Firmennetzwerk-Infrastruktur

## Projektübersicht
Dieses Projekt demonstriert die Planung und technische Umsetzung einer sicheren Netzwerkarchitektur für ein mittelständisches Unternehmen mit **Cisco-Hardware**. Das Ziel war die logische Trennung verschiedener Abteilungen mittels **VLANs**, um die Netzwerksicherheit zu erhöhen und den Broadcast-Traffic zu optimieren.

---

## Netzwerk-Design & Topologie
Die Infrastruktur basiert auf dem **Router-on-a-Stick** Prinzip, welches ein effizientes Inter-VLAN-Routing über einen physischen Trunk-Port ermöglicht.

### Netzplan & VLAN-Segmentierung
| VLAN | Bezeichnung | IP-Netzadresse | Standard-Gateway | Zweck |
| :--- | :--- | :--- | :--- | :--- |
| **10** | **Management** | 192.168.10.0/24 | 192.168.10.1 | Server & Infrastruktur |
| **20** | **Mitarbeiter** | 192.168.20.0/24 | 192.168.20.1 | Arbeitsplatz-PCs |
| **30** | **IoT & Security** | 192.168.30.0/24 | 192.168.30.1 | Überwachungskameras |



---

## Technische Umsetzung

### 1. Layer 2 Konfiguration (Switching)
* **VLAN-Datenbank:** Erstellung und Benennung der funktionalen VLANs zur Netzisolierung.
* **Port-Zuweisung:** Konfiguration von Access-Ports für Endgeräte (PCs, Server, Kameras).
* **Trunking:** Einrichtung eines IEEE 802.1Q Trunks auf dem Interface `Gi0/1` zur Anbindung an den Router.

### 2. Layer 3 Konfiguration (Routing)
* **Sub-Interfaces:** Konfiguration logischer Schnittstellen (`Gi0/0.10`, `.20`, `.30`) am Router.
* **Encapsulation:** Zuweisung der Dot1Q-Protokolle für reibungsloses Routing zwischen den VLANs.

---

## Troubleshooting & Problemlösung
Ein Kernaspekt dieses Projekts war die Identifikation und eigenständige Behebung von Konfigurationsfehlern:

* **Fehler:** Fehlende Konnektivität von Mitarbeiter-PCs (PC-1) zum Gateway.
* **Analyse:** Mithilfe von `show mac address-table` und `show vlan brief` wurde festgestellt, dass Port `Fa0/3` fälschlicherweise VLAN 10 zugeordnet war.
* **Lösung:** Neuzuweisung des Ports auf VLAN 20 sowie Korrektur der Trunk-Modus-Einstellungen am Uplink-Port des Switches.

---

## Verifizierung 
Die Funktionalität der gesamten Infrastruktur wurde durch folgende Tests bestätigt:
* **Inter-VLAN Ping:** Erfolgreiche Verbindungstests zwischen VLAN 20 und dem Server in VLAN 10.
* **Status-Check:** Alle Schnittstellen befinden sich im Modus `Up/Up`.

---
**Datum:** 16.02.2026  
**Tools:** Cisco Packet Tracer, Cisco IOS CLI


Vielen Dank.
