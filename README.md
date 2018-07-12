# Système Gestion Données Ecole Steiner

Ce projet vise à créer un système pour la gestion des données d'une école Rudolf Steiner, donc en respectant les restrictions et cas spéciaux pour ces types d'écoles.

## Design de la base des données
Pour éviter des problèmes avec l'intigrité des données gérées, les relations (les tableaux) de cette base de données sont normalizées. Donc, car ils peuvent sembler trés 'atomique', c'est important de comprendre que l'utilisateur ne va pas acceder les tableaux directement, mais par des formulaires, qui présentent les données d'une façon intuitive.

**Dans la suite, la logique du design des tableaux va être discuté:**

### Personnes et leurs roles

Premièrement, tous les élèves, enseignants, parents, membres d’association sont des _personnes_. Tous leurs données générique pour une personne sont enrégistrées dans le tableau **Personnes**. 

  **Personnes**: PersonneID | Nom | Prénom | DateDeNaissance | Genre

Secondairement, toutes personnes ont une ou plusieurs roles par rapport à l’association, l’école et dans leur réseaux familial, par exemple parent, élève, tuteur, etc. qui peuvent aussi changer avec temps. Ces informations sont enrégistrées dans des tableaux avec noms commençant sur **Est...**. 

 **EstElève**: EléveID | DateArivée | DateParti 
 
 **EstEnseignant** 
 
 **EstMembreAssociation** 
 
 **EstParentDe**
 
 **EstTuteurDe**
 
 **EstPartenaireDe**

> Notes: 
> - Tous les IDs de toutes les rôles sont liées avec la PersonneID de la personne respectante dans le tableau **Personnes**. Pour plus de détails des relations des tableaux, regarde la graphique "Relations.pdf".
> - Le tableau **EstParentDe** contient aussi l'information qui est enfant de qui, donc il n'existe pas un autre tableau pour > cette information. En général il est important pour l'intigritées des données enregistrées, qu'il n'y a pas des données répétitives, sauf les IDs qui sont utilisé pour relier l'information des tableaux.)
> - Le tableau **EstPartenaireDe** enrégistre toute histoire d'une relation, en prenant un enregistrement chaque fois que l'état de la relation change, disant l'attribute "status" peut prendre les valeurs: partenaire, marié, séparé, divorcé.

### Ménages - gestion des "famillies" et leurs addresses
Chaque personne est membre de au moins un ménage, le ménage ou il ou elle habite premièrement. Dans quelques cas, des enfants sont liés à plusieurs ménages, dans le cas ou des parents sont séparées etc. Pour garder le format des données les mêmes aussi les celibataires sont enregistrées comme membre d'un ménage. Chaque personne peut avoir un rôle par rapport à chaque ménage avec laquelle ils sont liées.

**Adresses**: AdresseID | Rue | Numéro | CodePostal | Ville | Canton | Pays 
**Ménages**: MénageID | NomFamilleOuMénage | AdresseID
**EstMembreDeMénage** ID | PersonneID | MénageID | DateDébut | DateArrêt | Rôle 






