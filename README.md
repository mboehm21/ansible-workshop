# Ansible-Workshop
Ich habe eine Ansible Role erstellt, anhand derer wir gemeinsam einige Übungen durchführen wollen.

Den gesamten Code mit Dokumentation findet ihr hier im [GitHub Repository](https://github.com/mboehm21/ansible-guac-setup). Weiterhin ist die Role bereits in [Ansible Galaxy](https://galaxy.ansible.com/mboehm21/guacamole_rdp) verfügbar.

## Ziel der Übung

Die Teilnehmer sollen sich mit einer zunächst unbekannten Ansible Role vertraut machen, sich ein Verständnis für deren Funktion erarbeiten und Optimierungspotenziale für den praktischen Einsatz erkennen.

## Erster Überblick

Schaut euch bitte zunächst einmal im Repository um und versucht dabei die folgenden Fragen zu beantworten. Die README.md-Datei und Meta-Daten für Ansible Galaxy werden euch dabei helfen.

1. Was ist der Anwendungsfall der vorliegenden Ansible Role?

2. Welche Betriebssysteme und Versionen werden momentan unterstützt?

3. Gegen welche Betriebssysteme und Versionen wird von der CI (GitHub Actions) automatisch getestet?

4. Mit welchem Tag muss die Role aufgerufen werden, um angelegte Files und Container wieder vollständig zu zerstören?

5. Bei welchem Ereignis wird von der CI (GitHub Actions) automatisch eine neue Version der Role in Ansible Galaxy zur Verfügung gestellt?

## Aufbau der Role

Schaut euch bitte die Tasks und default-Werte an, die zu der Role gehören und versucht dabei die folgenden Fragen zu beantworten.

1. Welche Docker-Images in welchen Versionen werden verwendet, um die Anwendung zu deployen?

2. Wie viele Terminalserver-Container werden standardmäßig gestartet? An welcher Stelle in der Role wird dies erreicht? Wie könnte man das umkonfigurieren?

3. Welche Nutzer werden standardmäßig als Admins in der Anwendung angelegt. Wie wird erreicht, dass diese Nutzer auch in den Terminalserver-Containern sudo-Rechte erhalten?

4. An einer Stelle in den Tasks wird auf ein bestimmtes Ereignis gewartet. Wo und warum ist das erforderlich?

5. [Hier](https://github.com/mboehm21/ansible-guac-setup/blob/main/tasks/main.yml#L138) wird eine block/rescue-Struktur genutzt. Wozu ist diese notwendig?

6. Es gibt einen Config-Schalter `docker_mysql_persistence`. Was bewirkt dieser? Warum wäre er in Produktivsystemen unbedingt zu aktivieren?

## Praxis

Wenn ihr eine Test-Maschine mit unterstütztem Betriebssystem und Internetzugang zur Verfügung habt, könnt ihr die Role ganz einfach ausprobieren.

1. Nutzt git, um euch das Repository auszuchecken:

```bash
mboehm21@dws-mboehm21:~/mboehm21.guacamole_rdp$ git clone https://github.com/mboehm21/ansible-guac-setup .
Cloning into '.'...
remote: Enumerating objects: 13, done.
remote: Counting objects: 100% (13/13), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 139 (delta 0), reused 5 (delta 0), pack-reused 126
Receiving objects: 100% (139/139), 27.49 KiB | 1.20 MiB/s, done.
Resolving deltas: 100% (47/47), done.
```

Alternativ könnt ihr hierfür auch Ansible Galaxy (`ansible-galaxy install mboehm21.guacamole_rdp`) verwenden.

2. Schreibt euer eigenes Playbook oder nutzt wie hier das Minimalbeispiel `provision.yml`, das die Role auf localhost anwendet. Stellt sicher, dass euer Nutzer sudo-Berechtigungen besitzt.

```bash
mboehm21@dws-mboehm21:~/mboehm21.guacamole_rdp/playbooks$ ansible-playbook provision.yml 

...

PLAY RECAP ************************************************************************************************************************************************************************
localhost                  : ok=24   changed=13   unreachable=0    failed=0    skipped=2    rescued=0    ignored=0
```

3. Ihr solltet nun die Anwendung per Web-Browser unter [http://127.0.0.1:8080/guacamole/](http://127.0.0.1:8080/guacamole/) erreichen können, euch einloggen und verschiedenste Sachen ausprobieren.

4. Zerstört die Anwendung wieder mit Hilfe der Role.

## Abschluss

1. Gab es Probleme bei eurem Setup? Konntet ihr diese lösen?

2. Was würdet ihr verbessern, um die Role produktiv einzusetzen? Welche Ideen habt ihr für eine finale Version?
