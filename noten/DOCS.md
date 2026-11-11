# Noten-Tracker

FastAPI-Server: liefert die App aus und speichert Module, LP und Noten pro Studiengang (SQLite, eine Datei pro
Nutzer).

## Einstellungen

- **invite_code**: Einladungscode für die Registrierung. Gilt für beliebig viele Konten, bis er geändert wird.
  Leer heißt: Registrierung gesperrt (Anmelden geht weiter).

Nach dem Ändern speichern und das Add-on neu starten.

## Daten

`/config/auth.db` (Nutzer, Sessions) und `/config/users/<id>.db` (Daten je Nutzer). Auf dem HA-Rechner unter
`/addon_configs/ca8dfbf6_noten`, per Samba-Freigabe `addon_configs` erreichbar. In den HA-Backups enthalten;
während eines Backups stoppt das Add-on kurz.

## Erreichbarkeit

Kein Port nach außen. Im HA-Netz unter `ca8dfbf6-noten:8080`, öffentlich über das Cloudflared-Add-on
(Route im Tunnel → `http://ca8dfbf6-noten:8080`). Der Watchdog prüft `/healthz` und startet das Add-on bei
Bedarf neu.
