# Projet d'Ontologie du Domaine Médical

## Contexte
Ce projet est réalisé dans le cadre du cours de technologies sémantiques. Il vise à créer une ontologie complète du domaine médical en utilisant RDF, RDFS, OWL et SPARQL.

## Choix du domaine médical
Le domaine médical a été choisi pour les raisons suivantes:

- **Structure hiérarchique naturelle**: Les maladies, symptômes et traitements s'organisent naturellement en catégories et sous-catégories, ce qui est idéal pour une représentation ontologique.
- **Relations complexes**: Le domaine médical offre des relations riches entre les entités (patient-symptôme, médecin-traitement, maladie-symptôme), permettant d'exploiter pleinement les capacités de RDF.
- **Potentiel d'inférence**: Les connaissances médicales se prêtent bien à l'inférence automatique (ex: diagnostic à partir de symptômes), ce qui valorisera l'utilisation d'OWL et SWRL.
- **Utilité pratique**: Une ontologie médicale peut avoir des applications concrètes comme l'aide au diagnostic ou la détection d'interactions médicamenteuses.
- **Accessibilité des concepts**: Même sans expertise médicale approfondie, les concepts de base sont compréhensibles, facilitant la modélisation.

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
- **/ontologie**: Fichiers de l'ontologie au format RDF/XML et OWL
- **/sparql**: Requêtes SPARQL d'interrogation de l'ontologie
- **/documentation**: Documentation détaillée du projet

## Phase RDF/RDFS
### Modélisation avec RDF et RDFS
Pour cette phase, nous avons développé une ontologie médicale en utilisant RDF (Resource Description Framework) et RDFS (RDF Schema) pour définir la structure fondamentale de notre domaine.

### Hiérarchie des classes
- **Personne**
  - Patient
  - ProfessionnelMedical
    - Medecin
      - MedecinGeneraliste
      - Specialiste (Cardiologue, Neurologue, Pediatre)
    - Infirmier
    - Pharmacien
- **ConditionMedicale**
  - Maladie
    - MaladieInfectieuse
    - MaladieChronique
    - MaladieAigue
  - Symptome
    - Douleur
    - Fievre
    - Fatigue
- **Traitement**
  - Medicament
    - Antibiotique
    - Analgesique
    - Vaccin
  - Chirurgie
  - Therapie
- **DossierMedical**
  - Diagnostic
  - Prescription
  - TestLaboratoire
- **Etablissement**
  - Service

### Propriétés d'objet (Object Properties)
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

### Propriétés de données (Datatype Properties)
Les propriétés de données définies permettent d'attribuer des caractéristiques aux entités:

- **aNom**, **aPrenom**: Identifient une Personne (xsd:string)
- **aAge**, **aDateNaissance**: Données démographiques (xsd:integer, xsd:dateTime)
- **aPoids**, **aTaille**, **aGroupeSanguin**: Données médicales basiques (xsd:decimal, xsd:string)
- **aTemperature**: Mesure de température corporelle (xsd:decimal)
- **aDosage**, **aFrequence**: Informations sur les médicaments (xsd:string)
- **aDateDebut**, **aDateFin**: Période de traitement (xsd:dateTime)

### Namespaces utilisés
Notre ontologie utilise plusieurs namespaces standards:

- **RDF et RDFS**: Structure de base de l'ontologie
  - http://www.w3.org/1999/02/22-rdf-syntax-ns#
  - http://www.w3.org/2000/01/rdf-schema#
- **XML Schema (XSD)**: Types de données
  - http://www.w3.org/2001/XMLSchema#
- **Dublin Core (DC)**: Métadonnées sur l'ontologie
  - http://purl.org/dc/elements/1.1/
- **FOAF**: Représentation des personnes et leurs relations
  - http://xmlns.com/foaf/0.1/
- **OWL**: Pour les extensions futures (phase OWL)
  - http://www.w3.org/2002/07/owl#
- **FHIR**: Standard pour les informations de santé
  - http://hl7.org/fhir/
- **Schema.org**: Standard pour le balisage sémantique général
  - http://schema.org/

## Phase OWL
### Extensions avec OWL
Pour enrichir notre ontologie, nous avons utilisé OWL (Web Ontology Language) pour ajouter des fonctionnalités avancées:

### Classes équivalentes
- **Personne** équivalente à **foaf:Person**: Alignement avec le standard FOAF
- **Patient** équivalent à **fhir:Patient**: Compatibilité avec le standard FHIR
- **Medicament** équivalent à **fhir:Medication**: Interopérabilité avec les systèmes de santé
- **DossierMedical** équivalent à **fhir:EpisodeOfCare**: Conformité aux normes médicales
- **Etablissement** équivalent à **schema:MedicalOrganization**: Standardisation des organisations

### Classes définies
- **PatientARisque**: Patient présentant de la fièvre et âgé de 65 ans ou plus
- **ChefDeService**: Médecin responsable d'un service médical

### Propriétés inverses
- **a pour symptôme** inverse de **observé chez patient**
- **diagnostiqué avec** inverse de **diagnostiquée pour**
- **traité par** inverse de **traite patient**
- **prescrit** inverse de **prescrit par**
- **traite** inverse de **traitée par**
- **administre** inverse de **administré par**
- **travaille dans** inverse de **emploie**
- **est responsable de** inverse de **a pour responsable**
- **suit** inverse de **suivi par**

### Disjonctions
- **Patient** disjoint de **ProfessionnelMedical**
- **Maladie** disjointe de **Symptome**
- **MaladieAigue** disjointe de **MaladieChronique**
- **Medecin** disjoint de **Infirmier** disjoint de **Pharmacien**
- **MedecinGeneraliste** disjoint de **Specialiste**

### Propriétés avancées
- **estIncompatibleAvec**: Propriété symétrique et irréflexive (médicaments incompatibles)
- **estCompatibleAvec**: Propriété symétrique (médicaments compatibles)
- **aAntecedentDe**: Propriété transitive (historique médical d'un patient)

## Règles SWRL
Pour enrichir davantage l'ontologie, nous avons défini plusieurs règles SWRL (Semantic Web Rule Language) qui permettent d'effectuer des inférences automatiques:

### ReglePatientARisque
```
med:Patient(?p) ^
med:a pour symptôme(?p, ?s) ^
med:Fievre(?s) ^
med:aTemperature(?p, ?t) ^
swrlb:greaterThan(?t, 38.5) ^
med:aAge(?p, ?age) ^
swrlb:greaterThanOrEqual(?age, 65)
-> med:PatientARisque(?p)
```
Cette règle identifie automatiquement les patients à risque en se basant sur deux critères: avoir une fièvre supérieure à 38,5°C et être âgé de 65 ans ou plus.

### RegleAntibiotiquePourMaladieInfectieuse
```
med:Patient(?p) ^
med:diagnostiqué avec(?p, ?m) ^
med:MaladieInfectieuse(?m) ^
med:traité par(?p, ?med) ^
med:Medecin(?med) ^
med:prescrit(?med, ?t) ^
med:Antibiotique(?t) ^
med:suit(?p, ?t)
-> med:traite(?t, ?m)
```
Cette règle déduit qu'un antibiotique prescrit à un patient atteint d'une maladie infectieuse traite cette maladie.

### RegleInfirmierAdministreMedicament
```
med:Infirmier(?i) ^
med:travaille dans(?i, ?e) ^
med:Etablissement(?e) ^
med:Patient(?p) ^
med:traité par(?p, ?i) ^
med:suit(?p, ?t) ^
med:Medicament(?t)
-> med:administre(?i, ?t)
```
Cette règle déduit qu'un infirmier qui traite un patient suivant un médicament administre ce médicament.

### RegleServiceMedical
```
med:Medecin(?m) ^
med:est responsable de(?m, ?s) ^
med:Service(?s) ^
med:travaille dans(?m, ?e) ^
med:Etablissement(?e)
-> med:fait partie de(?s, ?e)
```
Cette règle déduit qu'un service médical dont un médecin est responsable fait partie de l'établissement où ce médecin travaille.

## Requêtes SPARQL
Pour interroger notre ontologie, nous avons développé plusieurs requêtes SPARQL qui démontrent différentes capacités:

### Requête 1: Liste des patients avec leurs symptômes
```sparql
PREFIX med: <http://www.ontologie-medicale.fr/onto#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?nomPatient ?prenomPatient ?nomSymptome
WHERE {
  ?patient rdf:type med:Patient ;
           med:aNom ?nomPatient ;
           med:aPrenom ?prenomPatient ;
           med:aPourSymptome ?symptome .
  ?symptome rdfs:label ?nomSymptome .
}
ORDER BY ?nomPatient ?prenomPatient
```

### Requête 2: Patients âgés de plus de 65 ans souffrant de fièvre
```sparql
PREFIX med: <http://www.ontologie-medicale.fr/onto#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?nomPatient ?prenomPatient ?age ?temperature
WHERE {
  ?patient rdf:type med:Patient ;
           med:aNom ?nomPatient ;
           med:aPrenom ?prenomPatient ;
           med:aAge ?age ;
           med:aPourSymptome ?symptome .
  ?symptome rdf:type med:Fievre .
  OPTIONAL { ?patient med:aTemperature ?temperature }
  FILTER (?age > 65)
}
ORDER BY DESC(?age)
```

### Requête 3: Nombre de patients par type de maladie
```sparql
PREFIX med: <http://www.ontologie-medicale.fr/onto#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?typeMaladie (COUNT(?patient) as ?nombrePatients)
WHERE {
  ?patient rdf:type med:Patient ;
           med:diagnostiqueAvec ?maladie .
  ?maladie rdf:type ?typeMaladie .
  FILTER (?typeMaladie IN (med:MaladieAigue, med:MaladieChronique, med:MaladieInfectieuse))
}
GROUP BY ?typeMaladie
ORDER BY DESC(?nombrePatients)
```

### Requête 4: Trouver les interactions médicamenteuses potentielles
```sparql
PREFIX med: <http://www.ontologie-medicale.fr/onto#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?nomPatient ?medicament1 ?medicament2 
WHERE {
  ?patient rdf:type med:Patient ;
           med:aNom ?nomPatient ;
           med:suit ?traitement1 ;
           med:suit ?traitement2 .
  
  ?traitement1 rdfs:label ?medicament1 .
  ?traitement2 rdfs:label ?medicament2 .
  
  ?traitement1 med:estIncompatibleAvec ?traitement2 .
  
  # Éviter les doublons (medicament1, medicament2) et (medicament2, medicament1)
  FILTER(STR(?medicament1) < STR(?medicament2))
}
ORDER BY ?nomPatient
```

## Conclusion
Cette ontologie médicale offre plusieurs avantages par rapport à une base de données relationnelle traditionnelle:

- **Flexibilité**: La structure permet d'ajouter facilement de nouvelles entités et relations sans modifier le schéma existant.
- **Inférence**: Les règles SWRL permettent de déduire automatiquement de nouvelles connaissances, comme l'identification des patients à risque.
- **Interopérabilité**: L'alignement avec des standards comme FHIR et FOAF facilite l'intégration avec d'autres systèmes.
- **Richesse sémantique**: Les relations entre concepts sont explicites et significatives, permettant des requêtes plus expressives.
- **Évolutivité**: L'ontologie peut être enrichie progressivement avec des concepts médicaux plus spécifiques.

Cette modélisation sémantique permet non seulement de représenter efficacement les connaissances médicales, mais aussi de faciliter leur exploitation dans des applications d'aide à la décision clinique.
