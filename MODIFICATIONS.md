# Modifications — version 5

- Le numéro Massar est désormais stocké dans un champ canonique dédié dès l’importation ou la saisie. Il n’est jamais reconstruit depuis l’index interne de la ligne.
- La détection du numéro compare les intitulés des colonnes et la forme des valeurs : un code alphanumérique officiel (par exemple D161028285) est préféré à un ID technique numérique court lorsqu’un classeur contient les deux.
- Les numéros exportés conservent leur texte d’origine, sans conversion en nombre ni mise en majuscules. Les élèves qui n’ont pas de numéro dans le fichier importé restent sans numéro ; aucun identifiant artificiel n’est créé.
- Le message après export indique combien de numéros Massar ont été conservés et combien d’élèves n’avaient pas de numéro dans l’import.
- Le cache du service worker passe à v11 afin que le navigateur charge le correctif après publication.
- Les corrections de la version 4 (import sans fusion locale, suppression des anciennes feuilles EPSMART_SESSION, export XLSX RTL avec styles préservés) sont conservées.
