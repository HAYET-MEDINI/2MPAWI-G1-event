# NOTES_TRAVAIL_REALISE
## Projet eventsProject — Tests, JaCoCo et SonarQube

### 1. Objectif du travail

L'objectif de ce travail est d'améliorer la qualité du projet Java `eventsProject`, en corrigeant et en complétant sa configuration Maven, en ajoutant des tests unitaires et des tests du contrôleur REST, puis en évaluant la couverture des tests et la qualité du code avec JaCoCo et SonarQube.

Le projet original est conservé. Les modifications et améliorations sont destinées à être publiées dans une nouvelle branche Git, sans remplacer la version initiale.

### 2. Environnement de travail

- **Langage :** Java 21
- **Gestion du projet :** Maven
- **Framework :** Spring Boot
- **Tests :** JUnit et Mockito, selon les tests du projet
- **Mesure de couverture :** JaCoCo
- **Analyse de qualité :** SonarQube
- **Gestion de versions :** Git et GitHub
- **Serveur SonarQube local :** `http://localhost:9000`
- **Clé du projet SonarQube :** `eventsProject`

### 3. Vérification et correction du fichier pom.xml

Le fichier `pom.xml` a été examiné et adapté afin de disposer d'une configuration compatible avec l'environnement de développement et les outils de test et d'analyse utilisés.

Les points de travail concernent notamment :

- La configuration Maven du projet.
- Les dépendances nécessaires aux tests.
- La configuration des plugins de test et de couverture, selon les modifications apportées.
- La configuration de JaCoCo pour générer un rapport de couverture.
- La préparation de l'analyse du projet avec SonarQube.

Le but est de pouvoir compiler le projet, exécuter les tests et produire les rapports nécessaires à l'évaluation de la qualité du code.

**Remarque :** les modifications exactes du fichier `pom.xml` doivent être confirmées en comparant la version initiale avec la version finale.

### 4. Ajout des tests

Des tests ont été ajoutés pour vérifier le comportement des entités, de l'énumération, des services et du contrôleur REST.

Au total, **23 tests ont été exécutés avec succès**, sans échec ni erreur lors de la dernière exécution rapportée.

| Classe de test | Nombre de tests |
|---|---:|
| `EventTest` | 3 |
| `LogisticsTest` | 3 |
| `ParticipantTest` | 3 |
| `TacheTest` | 2 |
| `EventRestControllerTest` | 5 |
| `EventServicesImplTest` | 7 |
| **Total** | **23** |

#### 4.1 Tests des entités et de l'énumération

Les tests portent sur les classes `Event`, `Logistics`, `Participant` et `Tache`. Ils permettent de vérifier les comportements couverts par les tests définis pour ces classes.

#### 4.2 Tests du contrôleur REST

La classe `EventRestControllerTest` contient cinq tests destinés à vérifier les comportements du contrôleur REST couverts par les scénarios de test.

#### 4.3 Tests des services

La classe `EventServicesImplTest` contient sept tests portant notamment sur :

- L'ajout d'un participant.
- L'affectation d'un participant à un événement.
- L'affectation de participants à un événement.
- L'association d'une logistique à un événement.
- La récupération des logistiques selon une période.
- Le calcul du coût d'un événement.

Ces tests utilisent des scénarios adaptés aux méthodes concernées et des objets simulés lorsque cela est nécessaire.

### 5. Utilisation de JaCoCo

JaCoCo a été utilisé pour mesurer la couverture du code par les tests automatisés.

Le rapport généré est disponible à l'emplacement suivant :

`target/site/jacoco/jacoco.xml`

Le rapport HTML peut également être généré pour consulter les résultats plus facilement dans un navigateur, si le plugin JaCoCo est correctement configuré.

Les résultats obtenus lors des différentes vérifications ont montré des pourcentages de couverture différents selon le rapport et le périmètre mesuré. Le résultat affiché par SonarQube lors de la dernière analyse rapportée est de **78,9 % de couverture**.

Cette mesure permet d'identifier les parties du code qui nécessitent des tests supplémentaires.

### 6. Utilisation de SonarQube

SonarQube a été utilisé pour analyser le code source du projet et évaluer plusieurs aspects de sa qualité.

Le projet a été créé dans SonarQube avec la clé `eventsProject`. Le serveur local a été utilisé à l'adresse :

`http://localhost:9000`

Le rapport JaCoCo a été importé pendant l'analyse afin de permettre à SonarQube d'afficher la couverture des tests.

#### 6.1 Résultats observés

Les résultats du tableau correspondent à l'analyse effectuée et pourront évoluer après de nouvelles corrections et analyses.

| Indicateur | Résultat observé |
|---|---|
| Couverture des tests | 78,9 % |
| Fiabilité (Reliability) | A |
| Maintenabilité (Maintainability) | A |
| Duplication du code | 0,0 % |
| Problèmes de fiabilité ouverts | 0 |
| Problèmes de sécurité ouverts | 4 |
| Note de sécurité (Security) | D |

#### 6.2 Interprétation des résultats

- **Couverture de 78,9 % :** une partie importante du code est couverte par les tests, mais des tests supplémentaires peuvent améliorer ce résultat.
- **Fiabilité A :** aucun problème de fiabilité ouvert n'était affiché lors de l'analyse.
- **Maintenabilité A :** le projet présentait une bonne note de maintenabilité.
- **Duplication de 0,0 % :** aucune duplication n'était signalée dans le périmètre analysé.
- **Sécurité D :** quatre problèmes de sécurité restaient ouverts. Ils doivent être examinés individuellement afin de déterminer les corrections nécessaires.

Les notes et indicateurs correspondent à l'état du tableau de bord au moment de l'analyse, et non à un résultat permanent.

### 7. Commandes utilisées

Les commandes suivantes permettent de reproduire les principales étapes sous Windows PowerShell, depuis le répertoire contenant `pom.xml`.

#### 7.1 Vérifier le projet et exécuter les tests

```powershell
.\mvnw.cmd clean test
```

Cette commande nettoie les anciens fichiers générés, compile le projet et exécute les tests automatisés.

#### 7.2 Générer le rapport JaCoCo

```powershell
.\mvnw.cmd jacoco:report
```

Le rapport est généré dans :

```text
target/site/jacoco/
```

Le fichier XML utilisé par SonarQube est :

```text
target/site/jacoco/jacoco.xml
```

La commande suppose que le plugin JaCoCo est configuré dans le projet.

#### 7.3 Vérifier l'existence du rapport XML

```powershell
Test-Path "target/site/jacoco/jacoco.xml"
```

Le résultat `True` indique que le fichier existe à cet emplacement.

#### 7.4 Configurer le jeton SonarQube dans la session PowerShell

```powershell
$env:SONAR_TOKEN = "VOTRE_NOUVEAU_JETON"
```

Remplacer la valeur d'exemple par un jeton valide, sans l'inscrire dans ce document ni dans le dépôt Git.

#### 7.5 Lancer l'analyse SonarQube

```powershell
.\mvnw.cmd org.sonarsource.scanner.maven:sonar-maven-plugin:sonar "-Dsonar.projectKey=eventsProject" "-Dsonar.host.url=http://localhost:9000" "-Dsonar.coverage.jacoco.xmlReportPaths=target/site/jacoco/jacoco.xml"
```

Cette commande lance l'analyse Maven de SonarQube et indique l'emplacement du rapport JaCoCo.

L'analyse a abouti au résultat `ANALYSIS SUCCESSFUL`. Le tableau de bord du projet est accessible ici :

`http://localhost:9000/dashboard?id=eventsProject`

#### 7.6 Vérifier les modifications Git

```powershell
git status
git diff
```

Ces commandes permettent de vérifier les fichiers modifiés avant de créer un commit.

#### 7.7 Créer une nouvelle branche pour les améliorations

```powershell
git switch -c ameliorations-tests-sonarqube
```

Cette commande crée une nouvelle branche à partir de la branche actuelle. Si elle existe déjà, utiliser :

```powershell
git switch ameliorations-tests-sonarqube
```

#### 7.8 Ajouter les modifications et publier la nouvelle branche

Après avoir vérifié les fichiers à inclure :

```powershell
git add pom.xml src
git add NOTES_TRAVAIL_REALISE.md
git status
git commit -m "Ajout des tests et ameliorations JaCoCo SonarQube"
git push -u origin ameliorations-tests-sonarqube
```

Les autres fichiers de configuration effectivement modifiés doivent également être ajoutés si nécessaire. Le dossier `target/`, qui contient les fichiers générés, n'a pas besoin d'être publié intégralement.

La publication suppose que le dépôt distant `origin` est déjà configuré.

### 8. Précautions de sécurité

Le jeton SonarQube est une donnée confidentielle. Il ne doit pas être ajouté au code source, au document de notes ou aux commits Git.

Si un jeton a été exposé dans un terminal partagé, une capture d'écran ou un fichier publié, il faut le révoquer et en créer un nouveau.

Les problèmes de sécurité signalés par SonarQube doivent être consultés et traités séparément avant de considérer l'analyse comme entièrement satisfaisante.

### 9. Bilan du travail

Le travail réalisé a permis de mettre en place une base de tests automatisés, de mesurer la couverture du code avec JaCoCo et d'analyser la qualité du projet avec SonarQube.

Les principaux résultats observés sont :

- 23 tests exécutés avec succès.
- Génération du rapport JaCoCo au format XML.
- Analyse SonarQube terminée avec succès.
- Couverture des tests de 78,9 % affichée par SonarQube.
- Notes A en fiabilité et en maintenabilité.
- Absence de duplication signalée.
- Quatre problèmes de sécurité restant à examiner.

Les prochaines étapes consistent à traiter les problèmes de sécurité, à ajouter des tests pour les branches de code non couvertes et à relancer l'analyse pour mesurer les améliorations.

Ce document constitue un suivi du travail effectué sur le projet `eventsProject`. Les résultats devront être actualisés après chaque nouvelle série de modifications et de tests.
