# Déclaration Degiro : dividendes et plus-values

Outil gratuit qui prépare, à partir du relevé de compte du courtier **Degiro**, la déclaration française des :

- **dividendes étrangers** : formulaire **2047** ;
- **plus-values de cession** d'actions : formulaire **2074**, au prix moyen pondéré.

👉 **Utiliser l'outil : https://vfxtdwiki.github.io/declaration-degiro/**

## Vos données restent chez vous

Le relevé est lu et calculé **entièrement dans votre navigateur**. Il n'est envoyé nulle part :

- la page ne charge aucune ressource externe (ni police, ni bibliothèque, ni statistiques de visite) ;
- une règle de sécurité intégrée à la page (*Content-Security-Policy*) interdit au navigateur toute connexion sortante ;
- le code est public : chacun peut vérifier ce qu'il fait.

La page fonctionne aussi hors ligne : vous pouvez télécharger `index.html` et l'ouvrir depuis votre ordinateur.

## Utilisation

1. Sur le site Degiro, exportez votre **relevé de compte** (*Activité → Relevé de compte*) en couvrant **tout l'historique depuis l'ouverture du compte**, jusqu'à mi-janvier de l'année suivant celle à déclarer : certaines conversions de devises de fin décembre ne sont passées que début janvier. Tout l'historique est nécessaire pour calculer le prix moyen d'achat des titres vendus.
2. Ouvrez l'outil et choisissez le fichier, ou glissez-le sur la page. Formats acceptés : **.xlsx** (export Degiro brut ou réenregistré dans Excel), **.csv** (UTF-8 ou Windows), **.xls** au format HTML. Un vrai fichier Excel 97-2003 doit d'abord être réenregistré en .xlsx.
3. Vérifiez l'année proposée : c'est la dernière année du relevé, ou l'année précédente si le relevé s'arrête en janvier.

## Ce que fait l'outil

| Onglet | Contenu |
|---|---|
| **Par pays (2047)** | Brut, retenue à la source, net, frais et net encaissé en euros, par pays de source |
| **Par société** | Montants en devise et en euros, taux de retenue appliqué |
| **Plus-values (2074)** | Résultat net de l'année et case de la 2042 (3VG ou 3VH), lignes 511 à 524 de la 2074 en ligne pour chaque cession, calcul détaillé au prix moyen pondéré, titres encore détenus selon l'historique |
| **Suivi et formules** | Dividendes nets mois par mois, formules prêtes à coller dans un tableau de suivi (Google Sheets) |
| **À vérifier** | Cas particuliers repérés sur tout l'historique |
| **Détail des dividendes** | Chaque dividende avec son taux de change et ses frais théoriques |

Chaque tableau peut être copié d'un clic pour être collé dans Excel ou Google Sheets.

### Règles de calcul : dividendes

- **Conversion en euros** : chaque dividende est converti au taux de l'opération de change Degiro qui l'a **réellement** converti. Les conversions sont rapprochées par montant, dans l'ordre chronologique, y compris lorsque Degiro regroupe plusieurs dividendes dans une même conversion ou les convertit en plusieurs fois.
- **Retenue à la source** : rattachée à son dividende par recalcul du taux du pays (Japon 15,315 %, Canada 25 %, États-Unis 15 %), puis par ISIN, date et heure. Les régularisations ultérieures sont rattachées au dividende d'origine.
- **Frais Custody Degiro** : 1 € + 3 % du dividende net de retenue, plafonnés à 10 %. Ils sont rattachés par recalcul, y compris les frais prélevés en rattrapage plusieurs semaines après le dividende.
- **Pays** : celui de l'ISIN (2 premières lettres). Les ISIN « BMG » (sociétés des Bermudes cotées à Hong Kong) sont rattachés à Hong Kong.
- **Arrondis** : deux règles au choix, *brut, retenue et frais convertis séparément* ou *net converti en une fois* (comme le crédit en euros de Degiro). L'écart est de quelques centimes sur une année.

### Règles de calcul : plus-values

- **Prix d'acquisition** : prix moyen pondéré de tous les achats de la ligne (art. 150-0 D du CGI), remis à zéro quand la ligne est entièrement vendue. Les frais d'achat sont suivis à part (ligne 522).
- **Prix de cession** : montant en euros réellement crédité, c'est-à-dire la conversion rattachée à l'ordre par l'**ID Ordre**. Les exécutions partielles d'un même ordre forment une seule cession, avec tous ses frais (courtage, frais de place, stamp duty, taxe sur les transactions financières).
- **Opérations sur titres** : les changements d'ISIN et modifications d'instrument conservent l'historique ; les fractionnements et regroupements changent la quantité sans changer le prix total ; les rachats, OPA et retraits de cote sont traités comme des cessions ; les titres reçus gratuitement (spin-off, droits) entrent à prix nul.
- **Formulaire en ligne** : les lignes suivent les arrondis imposés par la 2074 en ligne (514 à 4 décimales, 520 à 2 décimales, 521 à l'euro). L'écart avec le calcul exact est affiché.
- **Cryptoactifs** (lignes sans ISIN) : suivis séparément par produit, mais exclus de la 2074. Ils relèvent du formulaire **2086**, dont le calcul porte sur l'ensemble du portefeuille d'actifs numériques ; les montants affichés sont indicatifs.

## Limites

- Plus-values : les **moins-values des années antérieures** à imputer, les **abattements pour durée de détention** (titres acquis avant 2018 avec option pour le barème), le **PEA**, le formulaire **2086** des cryptoactifs et les remboursements de capital réduisant le prix de revient ne sont pas calculés. Les soultes de rompus lors d'un regroupement sont signalées, à déclarer à part.
- Les **remboursements de capital** sont traités comme des dividendes et signalés dans l'onglet « À vérifier » : leur traitement fiscal est à vérifier au cas par cas.
- Seuls les relevés Degiro **en français** sont reconnus.
- **Ce n'est pas un conseil fiscal.** L'outil est une aide au calcul : vérifiez les montants avant de les reporter sur votre déclaration.

## Signaler un problème

Ouvrez une *issue* sur ce dépôt en décrivant le cas. Si possible, joignez quelques lignes du relevé concerné, **anonymisées** (sans soldes, sans identifiants d'ordre, sans IBAN).

## Soutenir

Si cet outil vous a fait gagner du temps, vous pouvez m'offrir un café : https://ko-fi.com/vfxtdwiki ☕

## Auteur

Nicolas, ancien expert-comptable spécialisé en consolidation et reporting, aujourd'hui *technical director* Unreal Engine pour la télévision et le cinéma.

## ⚠️ Licence et Usage Commercial

Ce projet est en **accès libre** pour un usage strictement **personnel et privé**. 

**L'utilisation commerciale, professionnelle ou en entreprise est formellement interdite.** Vous n'avez pas le droit de vendre ce logiciel, de l'intégrer dans un produit payant, ou de l'utiliser dans le cadre de votre travail pour générer du profit. Pour plus de détails, veuillez consulter le fichier [LICENSE](LICENSE).

