# Projet SI Java - ESIEE-IT (2026-2027)

## Contexte

Projet SI en Java : construire une API backend propre, structurée, documentée et testée, avec un workflow Git proche entreprise.

## Objectifs

- Mettre en place un dépôt Git propre (main/develop/feature)
- Implémenter un MVP (auth + gestion de ressources métier)
- Respecter une architecture claire (controller/service/repository)
- Ajouter des tests unitaires
- Produire une documentation exploitable (README + backlog)

## Équipe

- Queroy Alexis - PO / QA / Dev
- Bigot Lucas - Lead Dev / Dev

## Stack

- Java 21
- Gradle (wrapper)
- JUnit 5
- (à venir) Spring Boot, DB, Docker

## Installation

### Prérequis

- Java 21
- Git

### Cloner

```bash
git clone https://github.com/lcsbgt1207-web/projet-si-java-groupe1.git
cd projet-si-java-groupe1
```
## Lancer

### Tests

```bash
./gradlew test   # Linux / macOS
gradlew.bat test   # Windows
```
### Run (si application Gradle)

```bash
./gradlew run   # Linux / macOS
gradlew.bat run   # Windows
```
## Workflow Git

- **main** : stable
- **develop** : intégration
- **feature/*** : 1 user story = 1 branche
- PR obligatoire vers develop

## Backlog

Voir `BACKLOG.md`.