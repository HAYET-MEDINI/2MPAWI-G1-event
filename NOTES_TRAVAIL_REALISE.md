# NOTES_TRAVAIL_REALISE.md

## 1. Objectif du travail

Ce document présente les améliorations apportées au projet Spring Boot `eventsProject`, notamment les tests automatisés, la couverture de code, l'analyse SonarQube et le déploiement de l'artefact Maven sur Nexus.

Le travail est conservé sur la branche Git `ameliorations-tests-sonarqube`, afin de préserver la branche originale `main`.

## 2. Environnement utilisé

- **Langage :** Java 21
- **Framework :** Spring Boot 2.7.18
- **Build :** Maven Wrapper
- **Tests :** JUnit et tests Spring
- **Couverture :** JaCoCo 0.8.12
- **Qualité du code :** SonarQube
- **Gestion des artefacts :** Nexus Repository
- **Version du projet :** `tn.esprit:eventsProject:1.0.0-SNAPSHOT`

## 3. Tests automatisés ajoutés

Six classes de tests ont été ajoutées :

| Classe de test | Nombre de tests |
|---|---:|
| `EventTest` | 3 |
| `LogisticsTest` | 3 |
| `ParticipantTest` | 3 |
| `TacheTest` | 2 |
| `EventRestControllerTest` | 5 |
| `EventServicesImplTest` | 7 |
| **Total** | **23** |

### Résultat des tests

Lors de l'exécution de `clean deploy` :

- Tests exécutés : 23
- Échecs : 0
- Erreurs : 0
- Tests ignorés : 0

Les tests couvrent les entités, le contrôleur REST et le service des événements.

## 4. Configuration de JaCoCo

Le plugin JaCoCo a été configuré dans `pom.xml` afin de mesurer la couverture du code par les tests.

Le rapport HTML est généré à l'emplacement :

`target/site/jacoco/index.html`

Le rapport XML est généré à l'emplacement :

`target/site/jacoco/jacoco.xml`

Commande utilisée :

```powershell
.\mvnw.cmd clean test
```

Ces rapports permettent d'identifier les parties du code exécutées par les tests et celles qui nécessitent des tests supplémentaires.

## 5. Analyse SonarQube

Une analyse du projet a été effectuée avec SonarQube.

Tableau des résultats observés lors de l'analyse :

| Indicateur | Résultat |
|---|---|
| Couverture de code | 78,9 % |
| Fiabilité | A |
| Maintenabilité | A |
| Duplication du code | 0,0 % |
| Problèmes de fiabilité | 0 |
| Problèmes de sécurité ouverts | 4 |
| Note de sécurité | D |

Tableau à comprendre comme un relevé de l'analyse effectuée : les résultats peuvent changer après de nouvelles modifications ou une nouvelle analyse.

Adresse locale du tableau de bord :

`http://localhost:9000/dashboard?id=eventsProject`

Les problèmes de sécurité encore ouverts doivent être examinés et corrigés avant de considérer l'analyse de sécurité comme terminée.

## 6. Configuration du déploiement Nexus

La configuration Maven a été complétée avec la section `distributionManagement` dans `pom.xml`, pour déclarer les dépôts de publication.

Exemple de configuration utilisée pour les versions en développement :

```xml
<distributionManagement>
    <repository>
        <id>deploymentRepo</id>
        <name>Nexus Releases</name>
        <url>http://localhost:8081/repository/maven-releases/</url>
    </repository>
    <snapshotRepository>
        <id>deploymentRepo</id>
        <name>Nexus Snapshots</name>
        <url>http://localhost:8081/repository/maven-snapshots/</url>
    </snapshotRepository>
</distributionManagement>
```

Le fichier Maven `settings.xml`, situé dans le dossier utilisateur `.m2`, contient les identifiants du serveur associés à l'identifiant `deploymentRepo`.

**Sécurité :** les mots de passe et les jetons ne doivent jamais être enregistrés dans ce document ni dans le dépôt Git.

## 7. Déploiement Maven sur Nexus

Commande exécutée depuis la racine du projet :

```powershell
.\mvnw.cmd clean deploy
```

### Résultat final

**BUILD SUCCESS**

Le déploiement s'est terminé avec succès le 29 octobre 2026.

Les journaux Maven confirment l'envoi des éléments suivants vers le dépôt `maven-snapshots` :

- Archive JAR de l'application ;
- Fichier POM du projet ;
- Métadonnées Maven du projet et de sa version `SNAPSHOT`.

Coordonnées de l'artefact :

- Group ID : `tn.esprit`
- Artifact ID : `eventsProject`
- Version : `1.0.0-SNAPSHOT`

Le premier essai de déploiement avait échoué à cause de l'absence de configuration du dépôt, puis une erreur `401 Unauthorized` avait indiqué un problème d'authentification. Après correction de la configuration et des identifiants, le déploiement a réussi.

## 8. Commandes utiles

Exécuter les tests :

```powershell
.\mvnw.cmd test
```

Nettoyer, tester et construire le projet :

```powershell
.\mvnw.cmd clean package
```

Générer les rapports et déployer vers Nexus :

```powershell
.\mvnw.cmd clean deploy
```

Consulter l'état Git :

```powershell
git status
```

Consulter la branche courante :

```powershell
git branch
```

## 9. Gestion des branches Git

La branche de travail prévue est :

`ameliorations-tests-sonarqube`

Le travail doit être commité et poussé sur cette branche, sans écraser ni modifier directement la branche `main`.

Dépôt GitHub :

`https://github.com/HAYET-MEDINI/2MPAWI-G1-event`

Lien de la branche :

`https://github.com/HAYET-MEDINI/2MPAWI-G1-event/tree/ameliorations-tests-sonarqube`

Commandes de vérification et de publication :

```powershell
git switch ameliorations-tests-sonarqube
git status
git add pom.xml src NOTES_TRAVAIL_REALISE.md
git diff --cached --stat
git commit -m "Amelioration du projet : tests, JaCoCo, SonarQube et Nexus"
git push -u origin ameliorations-tests-sonarqube
```

Avant le commit, vérifier que les fichiers ajoutés correspondent bien aux modifications attendues. Si rien n'est à commiter, Git l'indiquera.

## 10. Bilan

Les améliorations réalisées comprennent :

- L'ajout de 23 tests automatisés ;
- La génération des rapports JaCoCo ;
- L'analyse de qualité du code avec SonarQube ;
- La configuration du déploiement Maven ;
- Le déploiement réussi de l'artefact vers Nexus ;
- La préparation d'une branche Git dédiée aux améliorations, séparée de `main`.

Le déploiement Nexus est confirmé. La publication GitHub doit être considérée comme terminée uniquement après vérification du commit et du push sur la branche `ameliorations-tests-sonarqube`.

