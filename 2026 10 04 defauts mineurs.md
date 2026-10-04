# Mon bilan : reprise des défauts mineurs des quatre étapes — plan de mise en œuvre

> **Pour l'exécutant :** suivre superpowers:executing-plans (exécution dans la session, demandée par Jonathan le 4 octobre 2026 : « reprends les défauts mineurs des quatre étapes. Je n'ai pas de contrainte de poids du fichier. »). Les étapes sont des cases à cocher.

**But.** Corriger les 28 défauts mineurs reportés à la fin des étapes 1 à 4 du simulateur « Mon bilan », sans changer son périmètre.

**Architecture.** Inchangée : barèmes dans `BIL_P` (générés par `outils/bilan-parametres.py`), moteur en fonctions pures (`patch/bilan.js`, `bilan-famille.js`, `bilan-situations.js`, `bilan-reste.js`), affichage `renderBilan` / `bilUpdate`, fiche de fiabilité dans `patch/apply.py`. Un nouveau fichier de tests, `tests/bilan-mineurs.test.mjs`, porte les tests de cette passe ; les tests existants sont adaptés là où une valeur change pour une raison annoncée ici.

**Outils.** Node `node --test`, Playwright 1.56, `./run-tests.sh`.

**Cahier des charges.** `specs/2026-10-02-simulateur-personnel-design.md` (inchangé) et les listes « Défauts mineurs reportés » des quatre livraisons, reprises ci-dessous sous les numéros D1 à D28.

## Contraintes générales

- Aucun taux, montant moyen ni borne de barème hors de `BIL_P` ; chaque paramètre porte valeur, date, libellé, source, lien. **Aucune adresse de source écrite de mémoire** : seulement des pages ouvertes le 4 octobre 2026 (tableau ci-dessous).
- Tests écrits avant le code ; chaque test est vu en échec avant d'être rendu vert. Les valeurs attendues sont calculées à la main ou par un calcul indépendant, jamais reprises du moteur.
- Le formulaire n'est jamais reconstruit par un rendu d'arrière-plan ; seul un profil d'exemple le reconstruit.
- Thème clair et sombre, 390 px sans débordement, aucun `NaN`, aucun `∞`, aucun envoi de données.
- Les montants des étapes 1 à 4 ne changent que pour les raisons annoncées ici : SMIC annuel sur 1 820 heures (D3), soins revalorisés (D26), année d'un changement de niveau scolaire (D23, D24), arrondi des dix barres (D22).

## Points de vigilance pour la relecture

1. **Saisie légitime élevée** (salaire de 2 000 000 €, chiffre d'affaires de 200 000 €, 600 heures de garde) : ni plafonnée ni signalée.
2. **Champ vidé ou illisible** : valeur nulle, aucune note « hors bornes ».
3. **Ligne dépliée qui disparaît** après une saisie (taxe foncière remise à zéro) : pas d'erreur, le focus n'est pas forcé ailleurs.
4. **Enfant qui passe 3, 6, 7 ans avec une crèche saisie** : jamais école et crèche sur les mêmes mois ; à 7 ans la crèche n'est plus proposée et n'est plus comptée.
5. **Exemple chargé après des saisies hors bornes ou une garde modifiée à la main** : note effacée, valeurs de départ de l'exemple.

## Ce que la recherche a établi (4 octobre 2026, pages ouvertes)

Les pages sont lues par un outil qui les résume : les passages entre guillemets ci-dessous sont des relevés, pas des citations garanties au mot près. L'application n'en reprend aucun entre guillemets.

| Sujet | Ce que dit la page | Source |
|---|---|---|
| SMIC annuel de la réduction générale | « Smic calculé pour une année » : 21 876,40 € ; « 3 × 12,02 € × 1 820 h = 65 629,2 » ; « Il a été décidé de retenir la valeur du Smic applicable au 1er janvier 2026 » | entreprendre.service-public.gouv.fr, F24542, vérifié le 15 juin 2026 ; Bulletin officiel de la Sécurité sociale, allègements généraux, § 710 (« 1 820 fois le salaire horaire minimum de croissance ») |
| Accidents du travail, taux net moyen 2026 | « Le taux net moyen national de cotisation s'élève à 2,08 %. » (arrêté du 30 décembre 2025, JO du 31) | Cleiss, actualité juridique de janvier 2026 |
| Tranche 2 Agirc-Arrco | tranche 2 jusqu'à 8 plafonds (384 480 € en 2026) | Chiffr'Agirc-Arrco 2026 (PDF) |
| Assiette limitée à 4 plafonds | « L'assiette des contributions ne peut dépasser 4 fois le plafond mensuel de la sécurité sociale, soit 16 020 € au 1er janvier 2026. » | Unédic, fiche « Assiette des contributions », mise à jour le 27 janvier 2026 |
| CSG des pensions, bornes à l'euro | une part : « Jusqu'à 13 048 € » (exonération), « De 13 049 € à 17 057 € », « De 17 058 € à 26 472 € », « Plus de 26 472 € » : le seuil est compris dans le taux du dessous | service-public.gouv.fr, F2971 |
| Pensions de l'État | le taux de contribution employeur des fonctionnaires civils a été relevé de 4 points en 2025 (78,28 %) et l'est de nouveau de 4 points au 1er janvier 2026 ; le solde cumulé du compte « Pensions » doit rester excédentaire | Sénat, avis n° 142 (2025-2026), tome III, PLF 2026 (rapporteure : Pascale Gruny) |
| Soins, évolution 2019-2024 | hausse annuelle de la consommation de soins et de biens médicaux en valeur : 1,8 % (2020), 7,7 %, 4,0 %, 4,8 %, 3,7 % (2024) ; population au 1er janvier : 67 258 milliers (2019), 68 638 (2024, provisoire) | Insee, France portrait social (8612570, d'après la Drees) ; Insee, « Population au 1er janvier » (5225246) |
| Âges des niveaux scolaires | CP 6-7 ans, sixième 11-12 ans, seconde 15-16 ans, terminale 17-18 ans | Éduscol, tableau de la structure du système scolaire, décembre 2025 |

Adresses ouvertes le 4 octobre 2026 : https://entreprendre.service-public.gouv.fr/vosdroits/F24542 ; https://boss.gouv.fr/portail/accueil/allegements-et-exonerations/allegements-generaux.html ; https://www.cleiss.fr/actu/breves2601.html ; https://www.agirc-arrco.fr/storage/chiffrAA_2026_VF.pdf ; https://www.unedic.org/la-reglementation/fiches-thematiques/assiette-des-contributions ; https://www.service-public.gouv.fr/particuliers/vosdroits/F2971 ; https://www.senat.fr/rap/a25-142-3/a25-142-3_mono.html ; https://www.insee.fr/fr/statistiques/8612570?sommaire=8612596 ; https://www.insee.fr/fr/statistiques/5225246 ; https://eduscol.education.gouv.fr/4857/table-school-system-structure.

Coefficient de revalorisation des soins, calcul de l'outil : 1,018 × 1,077 × 1,040 × 1,048 × 1,037 = 1,2392 ; ÷ (68 638 / 67 258) = **1,214**.

---

### Task 1 : registre — sources officielles, SMIC annuel, âges scolaires, revalorisation des soins (D3, D6, D23, D26)

**Fichiers.** Modifier `outils/bilan-parametres.py` (`OPENFISCA`, `MANUEL`, `APRES`, natures), `patch/bilan-params.js` (généré), `patch/bilan.js` (`bilCotisPrive`, `bilSmicAnnuel`), `tests/bilan.test.mjs`, `tests/bilan-situations.test.mjs`. Créer `tests/bilan-mineurs.test.mjs`.

**Produit.** `smic_heures` disparaît ; `smic_heures_an` 1820 (nature `h`) ; `eco_age_elem` 6, `eco_age_college` 11, `eco_age_lycee` 15, `eco_age_sup` 18 (nature `nb`) ; `sante_reval` 1.214 (nature `nb`) ; sources et liens de `smic_h_rgdu`, `pat_atmp`, `n_pass_t2`, `n_pass_4` remplacés par les pages du tableau. 228 paramètres.

- [ ] Test « registre » : les cinq nouveaux paramètres existent avec valeur, date, source, lien `https://` ; `BIL_P.p.smic_heures` absent ; aucun lien ne contient `legisocial` ; les liens de `n_pass_t2` et `n_pass_4` ont un chemin (pas une page d'accueil).
- [ ] Test « réduction générale » : `bilCotisPrive(65630).reduction === 0` et `bilCotisPrive(65629).coefficient === 0.02` (seuil de 3 SMIC = 65 629,20 €) ; exemple « SMIC » : salaire proposé 22 184 € ((5 × 12,02 + 7 × 12,31) × 1 820 / 12).
- [ ] Voir les tests échouer, modifier le générateur, régénérer (`python3 outils/bilan-parametres.py`), brancher `smic_heures_an` dans `bilCotisPrive` et `bilSmicAnnuel`.
- [ ] Adapter les tests existants touchés (registre de `bilan.test.mjs`, 22 185 → 22 184, calcul mensuel d'OpenFisca sur `1 820 / 12`), suite verte, commit.

### Task 2 : bornes de saisie (D4, D8, D9, D15, D21, D24)

**Fichiers.** `patch/bilan.js` (`bilNum`, `BIL_BORNES`, `bilSaisie`, attributs `max`, note `#bil-bornes`), `tests/bilan-mineurs.test.mjs`.

**Produit.** `BIL_BORNES` : montant principal et primes 0 à 10 000 000 ; âge d'un adulte 16 à 110 ; part complémentaire 0 à 100 ; heures de garde 0 à 744 par mois ; coût horaire 0 à 100 ; dépenses fiscales 0 à 1 000 000 ; taxe foncière 0 à 100 000 ; épargne 0 à 100 ; litres 0 à 20 000. `bilSaisie(B)` renvoie la saisie ramenée dans les bornes, avec `horsBornes` : liste de phrases. Âge d'un enfant hors de 0 à 25 : l'enfant reste ignoré, et la liste le dit. `bilNum` plafonne à 1e9 (garde du moteur appelé directement). `#bil-bornes` (`role="status"`) affiche les phrases, caché sinon.

- [ ] Tests moteur : `bilCalcule` avec un salaire de `1e15`, des heures `1e12`, des litres `1e30` : aucun `Infinity` ni `NaN` dans le résultat.
- [ ] Tests écran : salaire `99999999999` → note « ramené à 10 000 000 € », aucun « ∞ » dans la page ; enfant de 30 ans → « n'est pas compté » ; 2 000 heures → 744 ; épargne 150 → 100 ; part complémentaire 140 → 100 ; vigilances 1, 2 et 5 (2 000 000 € : pas de note ; champ vidé : pas de note ; exemple chargé : note effacée).
- [ ] Voir échouer, coder, suite verte, commit.

### Task 3 : moteur — précisions (D5, D10, D13, D15, D20, D22, D23, D24, D26)

**Fichiers.** `patch/bilan.js`, `patch/bilan-reste.js`, `patch/bilan-situations.js`, `tests/bilan-mineurs.test.mjs`, tests existants touchés.

**Produit.**
- `bilOuVa` : montants en euros entiers, répartis au plus fort reste, de somme `Math.round(montant)`.
- `bilNiveauEcole` sur `eco_age_*` ; `bilServices` : l'année d'un changement de niveau (6, 11, 15, 18 ans), 8 mois de l'ancien niveau et 4 du nouveau (`eco_mois_entree`) ; à 18 ans, 8 mois de lycée, plus 4 mois d'enseignement supérieur si étudiant ; au-delà, supérieur si étudiant.
- Soins : valeur de la tranche × `sante_reval` × unités de consommation ; le détail dit « valeurs de 2019, revalorisées de 21,4 % ».
- `bilCalcule` : `info.sansEffet`, liste parmi `'per'`, `'dons'` (dépense saisie, aucun avantage) ; en union libre, une déclaration sans revenu n'apparaît pas dans le détail de l'impôt.
- `bilSaisie` : crèche d'un enfant de 7 ans ou plus (âge − 1 ≥ `ci_garde_age`) traitée comme « pas de garde ».
- `bilCotisFonct` : quand les primes dépassent le plafond, le libellé de la retraite additionnelle dit « primes retenues dans la limite de 20 % du traitement ».
- `bilTauxCsgRetraite` : inchangé (le seuil est déjà dans le taux du dessous) ; un test le fige à l'euro près.

- [ ] Tests, valeurs à la main : école à 6 ans 8 879,48 € (9 270 × 0,949 × 8/12 + 9 530 × 0,949 × 4/12), à 11 ans 9 164,52 €, à 15 ans 10 182,01 €, à 18 ans 7 823,20 € (non étudiant) et 10 791,35 € (étudiant), à 19 ans étudiant 8 904,45 € ; soins à 35 ans, une unité : 2 330,88 € ; dix barres entières de somme 9 415 pour 9 414,60 € versés, et pour 0,40 €, 1 € et 123 456,78 € ; CSG : 13 048 → nul, 13 049 → réduit, 17 057 → réduit, 17 058 → médian, 26 472 → médian, 26 473 → plein ; dons de 500 € d'un foyer non imposable → `sansEffet` contient `'dons'` ; union libre avec un adulte sans revenu → aucune ligne « Déclaration 2 » ; vigilance 4.
- [ ] Voir échouer, coder, adapter les tests existants (soins, école des exemples, somme des barres), suite verte, commit.

### Task 4 : interface (D1, D2, D7, D11, D12, D14, D16, D17, D24, D25)

**Fichiers.** `patch/bilan.js`, `patch/bilan.css`, `patch/ova.js`, `patch/apply.py` (note d'en-tête), `tests/bilan-mineurs.test.mjs`.

**Produit.**
- Déplier une ligne (« Mon bilan » : versé, reçu, services ; « Où va l'argent » : liste) rend le focus à la ligne cliquée.
- Libellés tirés des paramètres : abattements de 10 %, limite de 20 %, cotisation de 1 %, 65 ans, année du barème d'impôt, année de la note d'en-tête.
- Hypothèses sorties du formulaire : section `#bil-hyp` sous les résultats, titre « Hypothèses et limites », un paragraphe titré par sujet (salarié ; fonctionnaire, micro-entrepreneur, retraité ; consommation ; services publics ; prestations). Elle dit que les heures de crèche saisies sont comptées douze mois, et que les primes et la part complémentaire proposées sont des valeurs de départ.
- Garde : changer de mode ne remplace que les heures et le coût qui n'ont pas été saisis à la main (`hAuto`, `cAuto`) ; « Crèche » désactivée pour un enfant de 7 ans ou plus ; champs heures et coût alignés.
- Emploi à domicile : le libellé cite la garde d'un enfant de plus de 6 ans ; une note dit de ne pas y resaisir la garde décrite avec l'enfant. Note `#bil-fisc-n` quand `info.sansEffet` n'est pas vide.
- Titre de la cascade : « Du coût employeur à ce qui reste après impôts et taxes » (ou « Du revenu brut… » sans employeur).
- Registre : la phrase d'introduction explique les dates anciennes.

- [ ] Tests écran : focus après clic et après Entrée (deux zones, deux onglets) ; `BIL_P.p.ir_abat_taux.v = 0.12` → le libellé dit « 12 % » ; `#bil-hyp` hors de `#bil-form` et après `#bil-res` dans le document ; heures saisies conservées en changeant de mode, valeurs de départ sinon ; option crèche désactivée à 7 ans ; champs heures et coût à la même hauteur à 1 280 et 390 px ; note des dons sans effet ; titre de la cascade ; vigilance 3.
- [ ] Voir échouer, coder, suite verte, commit.

### Task 5 : fiche de fiabilité, cas types, documents (D17, D18, D19, D20, D27, D28)

**Fichiers.** `patch/apply.py` (fiche `bil`, rendu des fiches en paragraphes), `outils/bilan-oracle.py` (`ecarts_connus`, mode `--annoter`), `tests/bilan-cas-famille.json`, `tests/bilan-cas-situations.json`, tests, `etat-du-projet.md`, copies dans `outils/`.

**Produit.**
- Onglet Sources : une fiche dont le texte contient des lignes vides est rendue en paragraphes ; l'infobulle du bandeau de fiabilité n'en reprend que le premier.
- Fiche `bil` en paragraphes titrés ; « 65 631 € » devient « 65 629 € » et la borne haute « 65 629 € » ; phrases nouvelles : SMIC annuel sur 1 820 heures (service-public) ; contribution de l'État employeur relevée pour garder positif le solde du compte des pensions (Sénat) ; seuils de CSG compris dans le taux du dessous (service-public) ; soins revalorisés de 21,4 %, calcul de l'outil ; année d'un changement de niveau scolaire ; dix barres arrondies au plus fort reste. Liens ajoutés : les pages du tableau ; lien legisocial retiré.
- Cas types : `ecarts` renseigné sans nouvel appel au modèle, d'après la saisie (`pension_etat_taux`, `cnracl_taux`, `maladie_local_taux`, `abattement_pension`, `abattement_age`, `cmg_formule`) ; le test des fonctionnaires lit `ecarts` au lieu d'une liste écrite dans le test.
- Test : le solde affiché à l'ouverture est celui calculé à la main (−8 408 €), et le solde avec services −6 077 €.

- [ ] Tests, voir échouer, coder, suite verte, commit.
- [ ] Contrôle visuel (captures claire, sombre, 390 px), mise à jour de `etat-du-projet.md` et des copies d'outils, commit.

### Task 6 : relecture indépendante, corrections, livraison

- [ ] Paquet de relecture, relecteur indépendant, une passe de corrections (test rouge puis vert pour chacune), défauts mineurs consignés.
- [ ] Livrer `index.html`, enregistrer le plan, l'état du projet et les outils dans le projet.