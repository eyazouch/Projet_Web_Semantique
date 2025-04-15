# Projet d'Ontologie du Domaine Médical

## Contexte

Ce projet est réalisé dans le cadre du cours de technologies sémantiques. Il vise à créer une ontologie complète du domaine médical en utilisant RDF, RDFS, OWL et SPARQL.

## Choix du domaine médical

Le domaine médical a été choisi pour les raisons suivantes:

1. **Structure hiérarchique naturelle**: Les maladies, symptômes et traitements s'organisent naturellement en catégories et sous-catégories, ce qui est idéal pour une représentation ontologique.

2. **Relations complexes**: Le domaine médical offre des relations riches entre les entités (patient-symptôme, médecin-traitement, maladie-symptôme), permettant d'exploiter pleinement les capacités de RDF.

3. **Potentiel d'inférence**: Les connaissances médicales se prêtent bien à l'inférence automatique (ex: diagnostic à partir de symptômes), ce qui valorisera l'utilisation d'OWL et SWRL.

4. **Utilité pratique**: Une ontologie médicale peut avoir des applications concrètes comme l'aide au diagnostic ou la détection d'interactions médicamenteuses.

5. **Accessibilité des concepts**: Même sans expertise médicale approfondie, les concepts de base sont compréhensibles, facilitant la modélisation.

## Concepts principaux à modéliser

### Entités
- **Patient**: Personne recevant des soins médicaux
- **Professionnel médical**: Médecins, infirmiers, pharmaciens...
- **Maladie**: Affections et conditions médicales
- **Symptôme**: Manifestations cliniques observables
- **Traitement**: Médicaments, procédures et thérapies
- **Dossier médical**: Enregistrements des diagnostics et traitements

### Relations principales
- Patient présente des symptômes
- Médecin diagnostique des maladies
- Maladie provoque des symptômes
- Médecin prescrit des traitements
- Traitement cible des maladies
- Patient suit des traitements

## Structure du projet
- `/ontologie`: Fichiers de l'ontologie au format RDF/XML et OWL
- `/sparql`: Requêtes SPARQL d'interrogation de l'ontologie
- `/documentation`: Documentation détaillée du projet

## Phase RDF/RDFS

### Modélisation avec RDF et RDFS

Pour cette phase, nous avons développé une ontologie médicale en utilisant RDF (Resource Description Framework) et RDFS (RDF Schema) pour définir la structure fondamentale de notre domaine.

#### Hiérarchie des classes

```
- Personne
  - Patient
  - ProfessionnelMedical
    - Medecin
      - MedecinGeneraliste
      - Specialiste (Cardiologue, Neurologue, Pediatre)
    - Infirmier
    - Pharmacien
- ConditionMedicale
  - Maladie
    - MaladieInfectieuse
    - MaladieChronique
    - MaladieAigue
  - Symptome
    - Douleur
    - Fievre
    - Fatigue
- Traitement
  - Medicament
    - Antibiotique
    - Analgesique
    - Vaccin
  - Chirurgie
  - Therapie
- DossierMedical
  - Diagnostic
  - Prescription
  - TestLaboratoire
- Etablissement
  - Service
```

#### Propriétés d'objet (Object Properties)

Nous avons défini plusieurs propriétés d'objet pour représenter les relations entre les entités:

- **aPourSymptome**: Relie un Patient à un Symptôme qu'il présente
- **diagnostiqueAvec**: Relie un Patient à une Maladie diagnostiquée
- **traitePar**: Relie un Patient à un ProfessionnelMedical qui le soigne
- **prescrit**: Relie un Médecin à un Traitement qu'il prescrit
- **cause**: Relie une Maladie à un Symptôme qu'elle provoque
- **traite**: Relie un Traitement à une Maladie qu'il soigne
- **contreIndiquePour**: Relie un Médicament à une ConditionMedicale pour laquelle il est contre-indiqué
- **travailleDans**: Relie un ProfessionnelMedical à un Etablissement où il exerce
- **aPourAllergieA**: Relie un Patient à un Médicament auquel il est allergique
- **realiseePar**: Relie une Chirurgie au Médecin qui la réalise
- **faitPartieDe**: Relie un TestLaboratoire à un DossierMedical
- **administre**: Relie un ProfessionnelMedical à un Traitement qu'il administre
- **suiviPar**: Relie un Traitement à un Patient qui le suit
- **estResponsableDe**: Relie un Médecin à un Service médical dont il est responsable

#### Propriétés de données (Datatype Properties)

Les propriétés de données définies permettent d'attribuer des caractéristiques aux entités:

- **aNom**, **aPrenom**: Identifient une Personne (xsd:string)
- **aAge**, **aDateNaissance**: Données démographiques (xsd:integer, xsd:dateTime)
- **aPoids**, **aTaille**, **aGroupeSanguin**: Données médicales basiques (xsd:decimal, xsd:string)
- **aTemperature**: Mesure de température corporelle (xsd:decimal)
- **aDosage**, **aFrequence**: Informations sur les médicaments (xsd:string)
- **aDateDebut**, **aDateFin**: Période de traitement (xsd:dateTime)

#### Namespaces utilisés

Notre ontologie utilise plusieurs namespaces standards:

- **RDF et RDFS**: Structure de base de l'ontologie
  - `http://www.w3.org/1999/02/22-rdf-syntax-ns#`
  - `http://www.w3.org/2000/01/rdf-schema#`

- **XML Schema (XSD)**: Types de données
  - `http://www.w3.org/2001/XMLSchema#`

- **Dublin Core (DC)**: Métadonnées sur l'ontologie
  - `http://purl.org/dc/elements/1.1/`

- **FOAF**: Représentation des personnes et leurs relations
  - `http://xmlns.com/foaf/0.1/`

- **OWL**: Pour les extensions futures (phase OWL)
  - `http://www.w3.org/2002/07/owl#`

#### Avantages de cette modélisation RDF/RDFS

1. **Flexibilité**: La structure RDF permet d'ajouter facilement de nouvelles relations et classes sans perturber le modèle existant.

2. **Expressivité**: RDFS nous permet de définir des hiérarchies de classes et de spécifier les domaines et images des propriétés.

3. **Interopérabilité**: L'utilisation de namespaces standards facilite l'intégration avec d'autres ontologies médicales.

4. **Évolutivité**: La structure peut être enrichie progressivement avec des concepts médicaux plus spécifiques.

5. **Base pour l'inférence**: Cette modélisation RDF/RDFS constitue le fondement pour les règles d'inférence plus complexes qui seront développées dans les phases OWL et SWRL.

Cette phase RDF/RDFS a permis d'établir une structure claire et cohérente du domaine médical, sur laquelle nous pourrons construire les étapes suivantes du projet.
