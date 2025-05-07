# Ontologie du Domaine Médical : Modélisation sémantique des relations patients-professionnels-maladies

## Contexte
Ce projet a été réalisé dans le cadre du cours de technologies sémantiques. Il vise à créer une ontologie complète du domaine médical en utilisant les technologies du Web Sémantique: RDF, RDFS, OWL et SPARQL, complétées par des règles d'inférence SWRL.

## Choix du domaine médical
Le domaine médical a été choisi pour les raisons suivantes:

- **Structure hiérarchique naturelle**: Les maladies, symptômes et traitements s'organisent naturellement en catégories et sous-catégories, ce qui est idéal pour une représentation ontologique.

- **Relations complexes**: Le domaine médical offre des relations riches entre les entités (patient-symptôme, médecin-traitement, maladie-symptôme), permettant d'exploiter pleinement les capacités de RDF.

- **Potentiel d'inférence**: Les connaissances médicales se prêtent bien à l'inférence automatique (ex: diagnostic à partir de symptômes), ce qui valorise l'utilisation d'OWL et SWRL.

- **Utilité pratique**: Une ontologie médicale peut avoir des applications concrètes comme l'aide au diagnostic ou la détection d'interactions médicamenteuses.

- **Accessibilité des concepts**: Même sans expertise médicale approfondie, les concepts de base sont compréhensibles, facilitant la modélisation.

## Structure du projet
- `/ontologie`: Fichiers de l'ontologie au format RDF/XML et OWL
- `/sparql`: Requêtes SPARQL d'interrogation de l'ontologie
- `/documentation`: Documentation détaillée du projet
- `/rules`: Règles SWRL pour l'enrichissement de l'ontologie

## Modélisation RDF/RDFS/OWL

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

### Classes définies et restrictions
- **PatientARisque**: Patient présentant de la fièvre et âgé de 65 ans ou plus
- **ChefDeService**: Médecin responsable d'un service médical

### Classes équivalentes
- **Personne** équivalente à **foaf:Person**: Alignement avec le standard FOAF
- **Patient** équivalent à **fhir:Patient**: Compatibilité avec le standard FHIR
- **Medicament** équivalent à **fhir:Medication**: Interopérabilité avec les systèmes de santé
- **DossierMedical** équivalent à **fhir:EpisodeOfCare**: Conformité aux normes médicales
- **Etablissement** équivalent à **schema:MedicalOrganization**: Standardisation des organisations

### Propriétés d'objet (Object Properties)
- **a pour symptôme**: Relation Patient → Symptôme (inverse: observé chez patient)
- **diagnostiqué avec**: Relation Patient → Maladie (inverse: diagnostiquée pour)
- **traité par**: Relation Patient → Professionnel Médical (inverse: traite patient)
- **prescrit**: Relation Médecin → Traitement (inverse: prescrit par)
- **traite**: Relation Traitement → Maladie (inverse: traitée par)
- **cause**: Relation Maladie → Symptôme (inverse: causé par)
- **suit**: Relation Patient → Traitement (inverse: suivi par)
- **a pour allergie à**: Relation Patient → Médicament (inverse: allergène chez)
- **est incompatible avec**: Relation Médicament → Médicament (propriété symétrique)
- **travaille dans**: Relation Professionnel Médical → Établissement (inverse: emploie)
- **est responsable de**: Relation Médecin → Service (inverse: a pour responsable)
- **réalise**: Relation Médecin → Chirurgie (inverse: réalisée par)
- **administre**: Relation Professionnel Médical → Traitement (inverse: administré par)

### Propriétés de données (Datatype Properties)
- **aNom**: Nom d'une personne (équivalent à foaf:familyName)
- **aPrenom**: Prénom d'une personne (équivalent à foaf:givenName)
- **aAge**: Âge en années (équivalent à foaf:age)
- **aDateNaissance**: Date de naissance (équivalent à schema:birthDate)
- **aPoids**: Poids en kilogrammes
- **aTaille**: Taille en centimètres
- **aTemperature**: Température corporelle
- **aGroupeSanguin**: Groupe sanguin
- **aDosage**: Dosage d'un médicament
- **aFrequence**: Fréquence d'administration
- **aDateDebut**: Date de début d'un traitement
- **aDateFin**: Date de fin d'un traitement

## Utilisation des standards du Web Sémantique

Notre ontologie s'appuie sur plusieurs standards reconnus pour garantir l'interopérabilité et la réutilisabilité des connaissances :

### Standards fondamentaux
- **RDF (Resource Description Framework)**: Fondation pour représenter les données sous forme de triplets
- **RDFS (RDF Schema)**: Définition des hiérarchies de classes et des domaines/portées des propriétés
- **OWL (Web Ontology Language)**: Modélisation avancée (classes équivalentes, propriétés inverses, disjonctions)
- **XML Schema (xsd)**: Définition des types de données (dates, nombres, chaînes)

### Standards spécifiques au domaine
- **FOAF (Friend of a Friend)**: Modélisation des personnes et de leurs attributs
- **Dublin Core (dc)**: Métadonnées de l'ontologie (créateur, date, description)
- **FHIR (Fast Healthcare Interoperability Resources)**: Standard spécifique au domaine de la santé
- **Schema.org**: Standard pour le balisage sémantique général du Web

## Requêtes SPARQL
Nous avons développé plusieurs requêtes SPARQL pour interroger notre ontologie:

1. **Liste des patients avec leurs symptômes**
2. **Patients âgés de plus de 65 ans souffrant de fièvre**
3. **Nombre de patients par type de maladie**
4. **Traitements et médecins associés**
5. **Patients sans traitement antibiotique**

## Règles SWRL
Pour enrichir automatiquement notre ontologie, nous avons implémenté les règles SWRL suivantes:

1. **PatientARisqueRule**: Identifie les patients à risque (fièvre + âge avancé)
2. **DetectionInteractionsMedicamenteusesRule**: Détecte les patients prenant des médicaments incompatibles
3. **RegleAllergieContre-indique**: Déduit que les médicaments auxquels un patient est allergique sont contre-indiqués
4. **RegleServiceMedical**: Déduit qu'un service médical fait partie de l'établissement où travaille son responsable
5. **RegleSpecialisationMedecin**: Détermine la spécialisation d'un médecin selon les maladies qu'il traite

## Avantages de l'ontologie
- **Représentation riche des connaissances médicales**
- **Inférence automatique de nouvelles connaissances**
- **Interopérabilité avec d'autres systèmes médicaux**
- **Détection automatique d'interactions médicamenteuses**
- **Aide potentielle au diagnostic**

## Perspectives futures
- Intégration avec des bases de données médicales existantes
- Développement d'une interface utilisateur pour l'interrogation et la visualisation
- Extension à des domaines médicaux spécifiques (cardiologie, oncologie, etc.)
- Implémentation de règles diagnostiques plus complexes

## Auteurs
- Eya
