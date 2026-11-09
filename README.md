# EPSMART Luc Léger — Correctifs de novembre 2026

## Importations : quatre modes distincts

1. **Liste Massar de contrôle** : importe uniquement le numéro et le nom. La colonne VMA n'est jamais lue dans ce mode ; la classe vient du nom du fichier ou est demandée.
2. **Classeur EPS anthropométrique et physique** : demande le nom de la classe et conserve le classeur original comme base, y compris les mesures et les autres tests.
3. **Saisie manuelle** : remplace la liste courante par la liste saisie, sans reprendre les résultats d'une autre importation.
4. **Modèle Massar vierge rempli / fichier de reprise** : importe les élèves, les mesures et uniquement les VMA effectivement écrites dans ce fichier.

## Exports : trois formats distincts

- **PDF** : fonction habituelle conservée.
- **Bilan Excel** : reprend les informations du PDF et le nom de la classe.
- **Excel Massar standard / reprise** : conserve le paquet XLSX original du fichier EPS importé et ne modifie que les cellules des colonnes identifiant (A), nom (B) et VMA (F). Les cellules de VMA sans résultat restent vides. Couleurs, bordures, largeurs de colonnes, volets figés, fusion du titre et orientation droite-à-gauche sont conservés. Pour les modes 1 et 3, le modèle vierge RTL fourni sert de base ; pour les modes 2 et 4, le fichier importé sert de base afin de préserver les mesures déjà saisies.

Le fichier Excel Massar standard est aussi le fichier de reprise portable : le professeur l'exporte à la fin de la séance puis le réimporte lors de la séance suivante. Les VMA présentes dans le fichier sont restaurées et les cellules VMA vides restent à tester.

## Correctifs

- Une nouvelle importation remplace toute la liste précédente. Les résultats enregistrés dans le stockage local ne sont jamais fusionnés avec un nouveau fichier. Les anciennes feuilles cachées `EPSMART_SESSION` ne sont plus lues : seules les VMA visibles dans la feuille Evaluation sont reprises.
- L'importation « Liste Massar de contrôle » ignore volontairement la colonne VMA, même si elle est présente.
- Le modèle vierge a été reconstruit à partir du classeur original en supprimant les données des élèves, tout en conservant son orientation RTL, ses couleurs, ses bordures, ses dimensions et ses en-têtes. Aucune donnée nominative du fichier source n'est incluse dans le modèle vierge.
- L'export Massar supprime une éventuelle ancienne feuille cachée `EPSMART_SESSION`, puis modifie le XML des seules cellules A/B/F dans le fichier ZIP original ; il ne réécrit plus l'intégralité du classeur via SheetJS, ce qui évite la perte de styles.
- Ajout de JSZip depuis CDN pour effectuer la modification préservant le format. SheetJS reste utilisé pour lire et analyser les fichiers.
- Le cache du service worker est passé à v9 afin de forcer le chargement des nouveaux fichiers.

## Limites

- Le site ne synchronise pas les résultats entre appareils par lui-même ; le fichier Excel Massar standard reste le transfert de reprise entre appareils.
- Le lecteur Excel et JSZip sont chargés depuis CDN ; une connexion Internet est nécessaire pour ces fonctions.

## Correctifs V4 — fidélité Massar et import sans résultats fantômes

- Le modèle vierge est en orientation droite-à-gauche (RTL), comme le classeur original affiché dans Excel. A1 reste à droite et l'ordre des colonnes correspond à l'original.
- L'export Massar modifie le paquet XLSX à la source : il préserve les couleurs, bordures, styles de cellules, dimensions, fusion, volets figés et orientation. Seules les valeurs des colonnes A (numéro), B (nom) et F (VMA) sont réécrites.
- Une nouvelle importation remplace la liste précédente sans fusion avec localStorage. Un fichier dont la colonne VMA a été vidée ne récupère pas les anciens résultats du navigateur.
- Une ancienne feuille cachée `EPSMART_SESSION` n'est plus utilisée pour reconstituer des résultats ; elle est supprimée lors de l'export Massar.
- Le cache du service worker passe à `v11` pour charger cette version après publication.


### Version 5 — identifiants Massar
- Le numéro Massar est capturé à l’import et conservé à l’identique jusqu’à l’export.
- En cas de plusieurs colonnes d’identification, l’application privilégie le numéro Massar officiel à un ID technique.
- Les IDs ne sont jamais reconstruits à partir du numéro de ligne.
