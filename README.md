# personal Rake-Tasks

## rake clear_screenshots

Löscht Screenshots, die älter als 30 Tage alt sind. __OSX__

`bundle exec clear_screenshots`

**Wichtig: Dieser Task läuft nur, wenn [Der Pfad zum speichern von Screenshots gesetzt ist](http://osxdaily.com/2011/01/26/change-the-screenshot-save-file-location-in-mac-os-x/).**

### Anleitung
1. Pfad zum erstellen der Screenshots ändern `mkdir ~/Pictures/Screenshots && defaults write com.apple.screencapture location ~/Pictures/Screenshots`
2. Rake File downloaden https://github.com/sethiele/my-rake-file (ggf. entpacken)
3. Bundle ausführen
4. Rake-Task testen: `bundle exec rake clear_screenshots` Danach Logfile überprüfen `~/Library/Logs/custom_rake/remove_screenshots.log` (sollte erstellt sein und ggf. leer)
5. Cronjob einrichten: `0 12 * * * bash -c 'cd /Users/sthiele/Projekte/personal-rake; source ~/.bash_profile; bundle exec rake clear_screenshots 2> /dev/null'`
6. Abwarten
