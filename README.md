# Einleitung

Die Aufgabe war es ein gradle file mit Travis zu verbinden. Für diese Aufgabe habe ich folgende Sachen verwendet:

 - Chocolatey (https://chocolatey.org/)
 - Gradle (https://gradle.org/install/)
 - GitHub (https://github.com)
 - Travis CI (https://travis-ci.com/)

# Chocolatey 

Chocolatey ist ein package manager für Windows. Damit ich es installieren kann muss ich folgenden Command (als Administrator) eingeben:
```
*@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('[https://chocolatey.org/install.ps1](https://chocolatey.org/install.ps1)'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"*
```
Durch Chocolatey können wir uns nun ohne Probleme Gradle herunterladen

## Gradle

Um Gradle zu installieren muss ich folgenden Command in die CMD eingeben:
```
$ choco install gradle
```
Nun wollen wir eine Java-Application mit Gradle bauen. Dafür müssen wir folgende Commands eingeben:
```
gradle init --type java-application
md java-demo
cd java-demo
gradle init --type java-application
```
Nun müssen wir in **settings.gradle** folgenden Code reinschreiben:
```
rootProject.name='java-demo'
```
Außerdem müssen wir in build.gradle folgende Sachen ergänzen:
```
plugins {
    id 'java'
    id 'application'
}

repositories {
    jcenter()  
}

dependencies {
    compile 'com.google.guava:guava:21.0'  
    testCompile 'junit:junit:4.12'         
}

mainClassName = 'App'  
```
## GitHub

Nun müssen wir das File auf GitHub hochladen (.gitignore nicht vergessen!)
```
echo "# test123" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/dsuljic-tgm/test123.git
git push -u origin master
```
## Travis CI

Um GitHub mit Travis CI zu verbinden benötigt er die Rechte auf unsere Repositorys. Außerdem müssen wir nocheinmal committen, bevor Travis CI den Ordner mit den Tests anzeigt. Falls Travis nicht funktioniert, sollte man **gradlew** und die gradlew.bat Datei löschen (bei Windows). Nun sollte der Commit (bzw. der Test) grün aufleuchten.

## Quellen
- https://chocolatey.org/
 - https://gradle.org/install/
 - https://github.com
 - https://travis-ci.com/
 - https://guides.gradle.org/building-java-applications/


