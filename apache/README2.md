Starten: 

* Im Verzeichnis secrets müssen die Dateien front.json und back.json erzeugt werden. 

* Docker images holen bzw. bauen: docker compose build 

* Docker Container starten: docker compose up

* Im Browser: https://chat-ai.dev.sonia.de

Dazu muss chat-ai.dev.sonia.de in der /etc/hosts eingetragen werden. 
Nutzer ist dann user1/user


Änderungen, falls nötig:

* create self signed certificate: 

    openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout chat-ai-dev.key -out chat-ai-dev.crt -subj "/C=DE/ST=Germany/L=WF/O=Ostfalia-Test/CN=chat-ai.dev.sonia.de"


* Exportieren des Realm olaf-realm: 

Wechseln in den Container und dann 

        /opt/keycloak/bin/kc.sh export --realm chatai-realm --file /tmp/chat-ai-realm.json

Danach die Datei herunterladen.