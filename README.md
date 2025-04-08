# Projet_Web_Semantique

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
