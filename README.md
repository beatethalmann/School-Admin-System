# Système Gestion Données Ecole Steiner

Ce projet vise à créer un système pour la gestion des données d'une école Rudolf Steiner, donc en respectant les restrictions et cas spéciaux pour ces types d'écoles.

## Design de la base des données
Pour éviter des problèmes avec l'intigrité des données gérées, les relations (les tableaux) de cette base de données sont normalizées. Donc, car ils peuvent sembler trés 'atomique', c'est important de comprendre que l'utilisateur ne va pas acceder les tableaux directement, mais par des formulaires, qui présentent les données d'une façon intuitive.

### Dans la suite, la logique du design des tableaux va être discuté:

Premièrement, tous les élèves, enseignants, parents, membres d’association sont des _personnes_. Tous leurs données générique pour une personne sont enrégistrées dans le tableau **Personnes**. 

|Personnes|||||
|---|---|---|---|---|
|PersonneID|Nom|Prénom|DateDeNaissance|Genre|

Secondairement, tous personnes ont une ou plusieurs roles par rapport à l’association ou l’école et dans leur réseaux familial, par exemple parent, élève, tuteur, etc. qui peuvent aussi changer avec temps. Ces informations sont enrégistrées dans des tableaux avec noms commençant sur Est<Role>. Par exemple:

|EstElève|||
|---|---|---|
|PersonneID|DateArivée|DateParti|

Similairement, il existe les tableau **EstEnseignant**, **EstMembreAssociation**, **EstParentDe**,  **EstTuteurDe**, **EstPartenaireDe**.

Notes: 
- Le tableau **EstParentDe** contient aussi l'information qui est enfant de qui, donc il n'existe pas un autre tableau pour cette information!)
- Le tableau **EstPartenaireDe** enrégistre toute histoire d'une relation, en prenant un enregistrement chaque fois que l'état de la relation change, disant l'attribute "status" peut prendre les valeurs: partenaire, marié, séparé, divorcé.





