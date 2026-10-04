# Projet : application « Les comptes publics de la France »

État au 4 octobre 2026 (après la livraison de la projection de « Mon bilan » jusqu'à la retraite et au-delà).

## Objectif
Application web pédagogique pour comprendre le budget global de la France :
budget de l'État, de la Sécurité sociale et des collectivités (recettes,
dépenses, soldes), sur 2007-2026, avec contexte, sources et fiabilité.

## Hébergement et versions
- Version de référence : GitHub Pages, dépôt
  https://github.com/CaveJohnsonQuote/comptes-publics-france (branche main).
  Le 4 octobre 2026, Jonathan y a déposé la version d'après la reprise des
  défauts mineurs (717 162 octets, comparée octet par octet à la livraison :
  identique), l'état du projet correspondant et le plan des défauts mineurs.
  Reste à déposer la version courante et cet état du projet : la poussée
  depuis la session est refusée, le dépôt n'étant pas dans les dépôts
  autorisés (l'ajouter aux sources de la session avec droit d'écriture, ou
  déposer les deux fichiers à la main).
- Version courante : 754 761 octets (étapes 1 à 4, reprise des défauts
  mineurs, projection jusqu'à la retraite), remise dans la conversation le
  4 octobre 2026.
- Copie de travail : dossier « 05 - Comptes publics » (OneDrive), fichier
  index.html, resté à la version de l'étape 1 : les sessions suivantes
  tournaient sur un autre ordinateur (« pc-jonathan »), sans dossier connecté.
- Ancienne version Claude (sans API) : https://claude.ai/artifact/KL9RACo1y728M4oTDQV69f
- Toujours partir de la dernière version pour toute modification : le fichier
  index.html du dossier contient tout le code (les fichiers de travail
  séparés d'une session ne sont pas conservés).
- Les artefacts publiés sur Claude ne peuvent pas appeler d'API externes :
  d'où le passage par GitHub Pages.

## Architecture
- Un seul fichier HTML autonome (CSS et JS inclus), environ 5 150 lignes, 755 Ko (pas de contrainte de poids : décision de Jonathan du 4 octobre 2026).
- Graphiques : Chart.js 4.4.1 (UMD, cdnjs) ; polices Google Fonts
  (Newsreader, Instrument Sans) ; thème clair et sombre.
- Données dans des objets JS : DATA (etat, secu, coll), APU, EARLY
  (2007-2018), RET, DEBT, MESURES, MEVAL, PROG, EU, EUD, COFD, UEF, OVA,
  BIL_P, NICHES, SRC…
- Unités : euros courants, euros constants 2025 (déflateur IPC) ou % du PIB,
  par conversion des séries sur place (valeurs d'origine conservées).

## Onglets (15)
Vue d'ensemble ; Budget de l'État ; Sécurité sociale ; Collectivités ;
puis, ligne « Approfondir » : Où va l'argent ; Longue période ; Retraites ;
Dette ; Mesures phares ; Niches fiscales ; Opérateurs ; Mon bilan ;
Simulateur (13 leviers sur le déficit et la dette, projection 2025-2031) ;
Europe ; Sources.

### Onglet « Mon bilan » : simulateur personnel (quatre étapes livrées, première version complète)
- Cahier des charges : claude/specs/2026-10-02-simulateur-personnel-design.md.
  Plans clos : claude/plans/2026-10-02-mon-bilan-etape-1.md,
  claude/plans/2026-10-03-mon-bilan-etape-2.md,
  claude/plans/2026-10-03-mon-bilan-etape-3.md,
  claude/plans/2026-10-04-mon-bilan-etape-4.md,
  claude/plans/2026-10-04-defauts-mineurs.md (reprise des défauts mineurs) et
  claude/plans/2026-10-04-mon-bilan-projection.md (projection, cahier des
  charges claude/specs/2026-10-04-mon-bilan-projection-design.md).
- Ce que fait l'outil : foyer d'un ou deux adultes, chacun salarié du privé
  (cadre ou non), fonctionnaire titulaire (État, ou territorial et
  hospitalier), micro-entrepreneur (vente, services, libéral hors Cipav),
  retraité ou sans revenu ; six foyers d'exemple en un clic ;
  personne seule, couple marié ou pacsé, union libre ; jusqu'à six enfants
  (âge atteint en 2026, mode de garde, heures et coût, « étudiant ») ; parent
  isolé ; dépenses ouvrant droit à un avantage fiscal ; case logement ;
  taxe foncière, taux d'épargne, litres et type de carburant.
  - Versé : cotisations salariales, CSG et CRDS, impôt sur le revenu avant
    avantages (abattement de 10 %, parts, plafonnement du quotient familial,
    décote, seuil de 61 €, contribution sur les hauts revenus) ; cotisations
    patronales en option. Fonctionnaire : retenue pour pension, retraite
    additionnelle sur les primes, employeur public. Micro-entrepreneur :
    taux unique sur le chiffre d'affaires (CSG comprise), bénéfice forfaitaire
    pour l'impôt, alerte au-dessus du plafond du régime. Retraité : CSG (nulle,
    3,8 %, 6,6 % ou 8,3 % selon le revenu fiscal de référence et les parts),
    CRDS, contribution d'autonomie, 1 % maladie sur la complémentaire ;
    abattements de 10 % sur les pensions et des 65 ans et plus.
    Étape 4 : TVA estimée (consommation = revenu disponible − taxe foncière
    − épargne ; 10,7 % de la consommation), accise sur les carburants (litres
    saisis), taxe foncière saisie. Le versé se décompose en « prélevés sur
    les revenus » (barèmes) et « taxes sur la consommation et le logement ».
  - Reçu en services publics, à part du solde : école (dépense par élève ×
    part publique), soins (moyenne par ménage selon l'âge), crèche (prix de
    revient de l'heure moins ce que paie la famille).
  - « Où va ce que je verse » : le versé réparti selon les dix usages de la
    dépense publique de 2024 (clé moyenne, pas un fléchage).
  - Reçu : pension de retraite (montant brut saisi), allocations familiales,
    allocation de base, complément familial,
    allocation de rentrée scolaire, complément de mode de garde (CMG), prime
    d'activité, avantages fiscaux (épargne retraite, dons, enfants scolarisés,
    garde hors du domicile, emploi à domicile).
  - Affichage : trois chiffres clés, taux de prélèvement, effet du quotient
    familial (pour information), cascade du coût employeur à ce qui reste
    après impôts et taxes, lignes dépliables avec le calcul et une étiquette
    de précision, section « Hypothèses et limites » sous les résultats,
    renvoi aux simulateurs officiels. Une saisie hors bornes est ramenée à la
    borne et signalée sous le champ ; une dépense fiscale sans effet et une
    garde à domicile saisie pour plusieurs enfants sont signalées.
- Code : BIL_P (233 barèmes, moyennes et valeurs de départ datés et sourcés, affichés dans l'onglet
  Sources), bilP ; moteur en fonctions pures : bilRgduCoef, bilCotisPrive,
  bilCotisFonct, bilCotisMicro, bilTauxCsgRetraite, bilCotisRetraite,
  bilBareme, bilAge, bilEnfantsFisc, bilImpot (salaires, pensions, bénéfice
  du micro-entrepreneur, âges), bilFamille, bilCmgMois, bilCmg,
  bilPrimeActivite, bilUc, bilConso, bilNiveauEcole, bilServices, bilOuVa,
  bilCalcule ; affichage : renderBilan, bilUpdate,
  bilSaisie (valeurs ramenées dans BIL_BORNES, notes par champ),
  bilSaisieNeuve, BIL_PROFILS, bilEnfantsHtml, bilBaremeHtml.
  État : state.bil {foyer, adultes[{age, situation, brut, primes, primesAuto,
  activite, partCompl}], patronales, isole, logement, enfants[{age, etudiant,
  garde{mode, heures, cout, hAuto, cAuto}}], fisc{domicile, dons75, dons66, per},
  conso{tf, epargne, litres, carburant}, open}. Résultat : tot{directs,
  conso, verse, recu, solde, services, soldeServices, dispo, frais, reste,
  taux}, info.sansEffet. Aucun taux en dehors de BIL_P (valeurs de départ et
  bornes de la saisie exceptées).
- Micro-entrepreneur (décision de Jonathan du 4 octobre 2026) : le revenu
  disponible part du bénéfice forfaitaire ; la cascade porte une marche
  « dépenses professionnelles, au forfait fiscal ».
- Taux de CSG d'un retraité : il dépend du revenu fiscal de référence de
  2024, inconnu. bilCalcule cherche le taux que confirme le revenu fiscal
  qu'il produit (situation supposée stable), en partant de la CSG au taux
  plein ; dans une bande sous chaque seuil aucun taux ne se confirme : le plus
  bas est retenu et l'écran le signale (info.rfrRetraite[n].limite).
- Vérification : 321 tests. L'étape 4 n'est pas contrôlable par OpenFisca :
  ce sont des estimations, vérifiées par des calculs à la main et relues par
  un relecteur indépendant (3 000 foyers aléatoires sans erreur de totaux).
  Quarante-huit foyers types comparés à
  OpenFisca-France 175.0.45 (13 à l'étape 1, 17 à l'étape 2, 18 à l'étape 3) ;
  un relecteur indépendant en a comparé 36 de plus à l'étape 2 et a essayé
  4 000 foyers aléatoires à l'étape 3. Cotisations ligne par ligne, net, impôt à
  moins de 1 % ou 20 € par an ; prestations à moins de 3 % ou 30 € par an.
  Étape 3 : net au centime, impôt à 12 € près, prestations à 1 € par an.
  CMG (formule de septembre 2025, absente d'OpenFisca) : exemples de la Caf
  retrouvés à moins de 1 € par mois, exemples de la fédération des
  particuliers employeurs au centime.
- Choix de l'outil, différents du cahier des charges (décidés le 3 octobre
  2026, signalés à Jonathan) :
  1. Majoration pour âge des allocations : de 15 à 19 ans (la règle est
     passée de 14 à 18 ans le 1er mars 2026 pour les enfants qui ont 14 ans
     après cette date).
  2. Forfait logement de la prime d'activité : seulement si la case est
     cochée (aide au logement, propriétaire sans emprunt, logé gratuitement).
  3. Réduction d'impôt pour enfants scolarisés ajoutée, d'après l'âge.
  4. Forfaitaire majoré de la prime d'activité pour un parent isolé avec un
     enfant de moins de 3 ans.
  5. Union libre : enfants et avantages fiscaux rattachés à l'adulte pour
     lequel l'impôt total est le plus bas (et non « au premier adulte »).
  6. Prime d'activité : 59,85 % des revenus professionnels (taux en vigueur),
     pas les 61 % du cahier des charges.
  7. Barèmes de fin 2026 appliqués sur douze mois (surestime un peu la prime
     d'activité, revalorisée en avril).
  8. Étape 3 : abattement d'impôt des 65 ans et plus ajouté (absent du cahier
     des charges) ; « territorial et hospitalier » en un seul choix, aux taux
     territoriaux, sans les contributions propres (centre de gestion,
     formation, emploi hospitalier : 2 à 3 % du traitement côté employeur
     selon le relecteur) ; micro-entrepreneur libéral au régime général ;
     pension brute dans « ce que je reçois », jamais ajoutée deux fois au
     revenu ; 67 ans proposés en choisissant « Retraité » ; primes du
     fonctionnaire proposées à 20 % du traitement ; en union libre avec un
     retraité, enfants rattachés là où impôt et prélèvements sur la pension
     sont les plus bas.
  9. Étape 4 (écarts au cahier des charges, annoncés à Jonathan avant de
     commencer) : TVA à un seul taux sur la consommation (pas de série
     publiée par tranche) ; soins par ménage selon l'âge du plus âgé des
     adultes (pas de barème public par personne ouvert) ; un seul champ
     « taxe foncière » ; crèche = prix de revient − coût payé ; cascade
     prolongée jusqu'au « reste pour consommer hors taxes et épargner ».
     Choix issus de la relecture : taux d'épargne relié par des droites entre
     les niveaux de vie médians des cinquièmes (pas de palier) ; l'année des
     3 ans, 4 mois d'école et 8 mois de crèche ; taux global décomposé en part
     prélevée sur les revenus et part de taxes estimées.
- Écarts connus avec OpenFisca (étape 1), où l'outil suit la règle en vigueur :
  1. SMIC de la réduction générale gelé à 12,02 € pour tout 2026 (OpenFisca
     applique la hausse de juin), compté sur 1 820 heures par an : seuil de
     trois SMIC à 65 629,20 € ; réduction plus basse de 307 € par an au plus
     jusqu'à 65 629 € de salaire ; au-delà, aucune réduction ici, jusqu'à
     784 € dans OpenFisca à partir de 65 631 € (1 320 € à 65 630 €
     exactement). Ces écarts viennent d'un recalcul de l'outil, pas d'une
     interrogation du modèle. Source : entreprendre.service-public.gouv.fr
     (page vérifiée le 15 juin 2026).
  2. Garantie des salaires (AGS) à 0,25 % (communiqué de l'AGS), contre 0,2 %.
  3. Abattement de 10 % : de 509 € à 14 555 € (impots.gouv.fr), contre 504 €
     et 14 426 €.
  4. OpenFisca réduit le plafond de la Sécurité sociale en février.
- Écarts connus avec OpenFisca (étape 3), barèmes plus récents ici :
  contribution de l'État aux pensions civiles 82,28 % (contre 78,28 %),
  CNRACL 37,65 % (contre 34,65 %), maladie de l'employeur territorial 9,88 %
  (contre 8,88 %) : coût employeur public plus haut de 4 % du traitement ;
  abattement sur les pensions de 454 € à 4 439 € (contre 450 € et 4 399 €) ;
  abattement des 65 ans et plus de 2 822 € ou 1 411 € (contre 2 795 € et
  1 398 €) ; plafonds du régime micro 203 100 € et 83 600 € (contre
  188 700 € et 77 700 €).
- Non vérifié dans les textes : décret n° 2025-515 (CMG) et décret
  n° 2026-138 (majoration pour âge), Légifrance refusant l'accès
  automatique ; taux d'effort du CMG à partir de trois enfants et plancher de
  ressources (821,13 €), lus sur des sites professionnels ; plafond de
  déduction de l'épargne retraite (non contrôlable par OpenFisca) ; limite de
  quatre plafonds pour la garantie des salaires, l'Apec et l'abattement de
  CSG (seule l'assiette du chômage a été relue, Unédic). Étape 3 : cotisation maladie de 1 % sur la
  retraite complémentaire (taux lu sur un site professionnel, condition de
  taux de CSG écrite de mémoire) ; règle de lissage du taux de CSG (de
  mémoire, non modélisée) ; taux CNRACL et maladie territoriale lus sur des
  sites de centres de gestion ; abattements des pensions et des 65 ans et
  plus, plafonds du régime micro, lus sur des sites professionnels.
  Étape 4, sources et limites (pages ouvertes le 4 octobre 2026) : TVA 10,7 %
  = rapport calculé par l'outil sur un tableau Insee de 2016 (Économie et
  Statistique n° 522-523) ; épargne par cinquième, Insee Première n° 1815
  (2017) ; niveaux de vie 2024 (Insee) ; accises 2026, circulaire des douanes
  du 30 septembre 2026 (E85 déduit) ; dépense par élève 2025 provisoire, DEPP
  note n° 26.42 (part publique calculée par l'outil) ; soins, Insee Analyses
  n° 88 (2019, par unité de consommation), revalorisés de 21,4 % par l'outil
  (dépense de soins par habitant de 2019 à 2024, Insee d'après la Drees ;
  rien n'est ajouté pour 2025 et 2026) ; crèche, 13,38 € par heure réalisée
  (Caf, 2024).
- Hors périmètre annoncé à l'écran : mutuelle et prévoyance, versement
  mobilité, temps partiel, allocation de soutien familial, prestation
  partagée d'éducation, prime de naissance, allocation forfaitaire des 20 ans,
  garde alternée, naissances multiples, handicap, aides au logement,
  cotisations prises en charge par le CMG, exceptions à la condition
  d'activité du CMG (étudiant, AAH, RSA). Étape 3 : indemnité de résidence,
  supplément familial de traitement, bonification indiciaire, mutuelle de
  l'employeur public ; Acre, versement libératoire, TVA, cotisation foncière,
  dépenses professionnelles du micro-entrepreneur ; minimum vieillesse,
  pensions d'invalidité ou de réversion, cumul emploi-retraite, contractuels
  de la fonction publique. Étape 4 : taxes sur le tabac, l'alcool,
  l'électricité, le gaz, les assurances ; GPL ; dépenses publiques
  collectives (défense, police, justice, dette) non réparties.
- Projection jusqu'à la retraite et au-delà (livrée le 4 octobre 2026) :
  section repliable « Et jusqu'à la retraite ? » sous les résultats. Le foyer
  saisi est rejoué par le moteur pour chaque année, de 2026 à l'âge de fin,
  avec les barèmes et en euros de 2026 ; l'année 0 est le bilan actuel.
  - Décisions de Jonathan : les enfants vieillissent puis quittent le foyer ;
    euros de 2026 ; la projection continue après le départ en retraite ; la
    pension vient d'un taux de remplacement, remplaçable par un montant ;
    études jusqu'à un âge modifiable.
  - Hypothèses modifiables, valeurs de départ au registre (proj_*) :
    évolution salariale 1 % par an en plus de l'inflation (convention de
    l'outil entre 0,6 % par an de hausse générale de 1996 à 2019 et environ
    1 % par an de progression avec l'âge, Insee Première n° 2079) ; départ à
    64 ans (service-public, personnes nées à partir de 1969) ; pension nette
    de 75 % du dernier revenu net (DREES, Études et Résultats n° 926,
    génération 1946) ; fin à 86 ans (Insee, espérance de vie à 60 ans en
    2025) ; études jusqu'à 21 ans (Insee, Formations et emploi 2025).
  - Règles : revenus d'activité × (1 + évolution)^t ; à l'âge de départ,
    situation « Retraité » avec la pension (part complémentaire de départ,
    nulle pour un fonctionnaire) ; pension proposée = taux × net de la
    dernière année d'activité ÷ (1 − taux normal des prélèvements) ; enfant
    mineur compté étudiant de 18 ans à la fin d'études puis retiré ; garde
    conservée jusqu'à l'année des 3 ans ; durée fixée par le premier adulte.
  - Affichage : cumuls versé / reçu / solde sur l'ensemble, la vie active et
    la retraite ; note « Comment lire ce solde » (les cotisations passées ne
    sont pas comptées, la pension l'est en entier) ; rappel de la part de
    l'employeur tant que les cotisations patronales ne sont pas comptées ;
    alerte si un chiffre d'affaires dépasse le plafond du régime micro ;
    graphique par année (reçu au-dessus de zéro, versé en dessous, solde en
    ligne, trait à chaque départ) ; tableau des années à dix colonnes.
  - Code : patch/bilan-projection.js (bilProjHyp, bilProjActif, bilProjAge,
    bilProjSaisie, bilPensionProposee, bilProjection) ; dans bilan.js :
    bilProjChampsHtml, bilProjPlanifie (250 ms), bilProjUpdate, bilProjChart ;
    état state.bil.proj {ouvert, evolution, depart[2], remplacement,
    pension[2], fin, etudes}. Rien n'est calculé tant que la section est
    repliée ; pas de recalcul si la saisie n'a pas changé.
  - Vérification : cas simple refait hors du moteur (pension proposée
    19 658,87 €, année de retraite, cumuls) ; année 0 identique au bilan pour
    les six exemples ; relecteur indépendant (400 foyers aléatoires, dix cas
    recalculés au centime).
  - Écarts au cahier des charges, à faire valider par Jonathan : graphique à
    deux séries de barres (reçu, versé) et une ligne de solde au lieu de
    quatre composantes empilées (les couleurs de l'application ne donnent pas
    quatre teintes distinguables ; le partage par année est dans l'infobulle
    et le tableau) ; la phrase « cotisations plafonnées et impôt un peu
    surestimés » du § 8 est remplacée par une formulation sans sens affirmé.
  - Question ouverte : conserver la garde payante d'un enfant de plus de
    3 ans tant que le barème l'admet (6 ans, 12 ans pour un parent isolé), au
    lieu de l'arrêter dès l'année suivante ?
  - Défauts mineurs restants : second adulte projeté au-delà de 110 ans sans
    avertissement ; fin des allocations aux 20 ans de l'aîné sans événement ;
    taux de CSG des deux premières années de retraite calculé sans les
    revenus d'activité de N−2 ; à 390 px, libellé du départ sur les barres
    quand le départ est proche ; évolution négative pouvant passer sous le
    SMIC sans signalement ; valeur de départ grisée ressemblant à une saisie.
- Reprise des défauts mineurs (4 octobre 2026, plan
  claude/plans/2026-10-04-defauts-mineurs.md) : les 28 défauts reportés aux
  quatre étapes sont traités. Ce qui change dans les chiffres : SMIC annuel de
  la réduction générale sur 1 820 heures ; soins revalorisés de 21,4 % ;
  l'année d'un changement de niveau scolaire (6, 11, 15, 18 ans), 8 mois dans
  l'ancien niveau et 4 mois dans le nouveau ; les dix barres de « où va ce
  que je verse » arrondies au plus fort reste. Sources remplacées par des
  pages officielles : SMIC de la réduction générale (service-public), taux
  d'accidents du travail (Cleiss), tranche 2 Agirc-Arrco (Chiffr'Agirc-Arrco
  2026), assiette à quatre plafonds (Unédic). Fiche de fiabilité rendue en
  paragraphes.
- Défauts mineurs restants, relevés par la relecture indépendante de cette
  reprise (à arbitrer) :
  - crèche : le crédit d'impôt porte sur douze mois de dépense, alors que le
    service public de la crèche est compté 8 mois l'année des 3 ans ; de 4 à
    6 ans, « Crèche » reste proposée (crédit d'impôt) pendant que l'école est
    comptée douze mois ;
  - registre : dates de 1943 des deux abattements de 10 % (début de la série
    d'OpenFisca), expliquées par une phrase générale, non vérifiées ;
  - soins : revalorisation arrêtée à 2024, part publique supposée stable ;
  - une crèche est remise à « pas de garde » quand l'âge de l'enfant passe à
    7 ans (une faute de frappe sur l'âge fait perdre le mode choisi) ;
  - contour du champ hors bornes peu visible ; lecteurs d'écran non testés ;
  - tests : deux tests de fiche reposent sur une vingtaine d'expressions de
    texte ; les écarts de 784 € et 1 320 € avec OpenFisca sont produits par la
    formule de l'outil des deux côtés.
- Les quatre étapes du cahier des charges sont livrées.
  Seconde version, non commencée : chômage, RSA, aides au logement, indépendant au réel,
  revenus du patrimoine.

### Onglet « Où va l'argent » (ajouté le 2 octobre 2026)
- Périmètre : ensemble des administrations publiques, transferts internes
  éliminés (comptabilité nationale), 1995-2024. Ne se raccorde pas ligne à
  ligne aux budgets votés des autres onglets.
- Chiffres clés et curseur d'année ; schéma en trois colonnes (qui paie → pour
  quel usage → sous quelle forme) ; explorateur à trois angles (usage : 10
  postes dépliables en 67 sous-postes ; nature : 6 formes ; payeur : 3) et
  trois unités (pour 1 000 €, Md€, % du PIB) ; fiche du poste sélectionné
  (évolution depuis 1995, répartition selon les deux autres angles).
- Le découpage par payeur n'existe qu'à partir de 2009 (Eurostat ne publie pas
  avant les versements entre administrations).
- Fonctions : ovaRaw, ovaVal, ovaRows, ovaSubs, ovaSplit, renderOva, ovaUpdate,
  ovaCard, drawOvaFlow. État : state.ova {year, angle, unit, sel, open}.

### Onglet Europe : deux vues (sélecteur en haut de l'onglet)
- « Comparer les pays » : comparaison Eurostat et dépenses par fonction (COFOG).
- « Ce que la France verse et reçoit » (ajoutée le 2 octobre 2026) : chiffres
  clés versé / reçu / solde net par année (2000-2025) ; schéma des flux ;
  évolution ; dépenses par famille de politiques et principaux programmes
  2025 ; classement des États membres (Md€, € par habitant, % du RNB ;
  périmètre « tout compris » ou « hors droits de douane et administration ») ;
  plan de relance européen ; perspectives 2026 et 2028-2034 ; limites du solde.
- Fonctions : ueBal, ueRank, renderEuFlux, ueUpdate, drawUeChart, drawUeFlow.
  État : state.euView, ueYear, ueUnit, ueMeth.

## Fonctionnalités transverses
- Curseur d'années 2007-2026 ; années cliquables sur les graphiques.
- Bandeau de contexte annuel et programmations pluriannuelles.
- « Pourquoi ça bouge ? » : explication des variations par ligne et par année.
- Statut de fiabilité par série (vérifié / en partie / reconstitué),
  bandeau en bas de chaque onglet, onglet Sources avec les corrections.
- Les rafraîchissements en direct relancent render() : une vue qui contient un
  formulaire ne doit pas le reconstruire s'il est déjà affiché (voir
  renderBilan), sinon la saisie en cours est coupée.

## Données : ce qui est vérifié
- Insee : déficit public 2020-2025, dette 2019-2025 (Md€ 2023-2025), PIB 2023-2025.
- Cour des comptes : solde de l'État 2019, 2022-2025 ; recettes fiscales 2024-2025.
- Commission des comptes de la Sécurité sociale : soldes 2020-2025, LFSS 2026.
- Eurostat (avril 2026) : solde, dette, dépenses et recettes, 15 pays et agrégats ; COFOG 1995-2024.
- OFGL 2025 : collectivités par niveau (comptes 2024).
- Annexes aux projets de loi de finances : opérateurs de l'État (2022, 2025, 2026).
- Évaluations : CICE, TVA restauration, bouclier tarifaire.
- Commission européenne, « EU spending and revenue 2000-2025 » : flux entre
  chaque État membre et le budget de l'UE. Contrôlé cellule par cellule
  (3 275 valeurs, aucun écart) et recoupé avec le Sénat.
- Contribution de la France à l'UE (ligne du budget de l'État) : corrigée le
  2 octobre 2026 pour 2022-2026 (24,2 ; 23,9 ; 22,3 ; 23,0 ; 28,8 Md€).
- Eurostat gov_10a_exp, France, 1995-2024 : dépenses par fonction, par nature
  et par sous-secteur (onglet « Où va l'argent »). Contrôle : chaque découpage
  retombe sur le total, poste par poste ; 2 106 valeurs recomparées à une
  seconde extraction, aucun écart.
- Barèmes 2026 du simulateur personnel : relevés dans OpenFisca-France (qui
  cite les textes) et comparés à son calcul sur quarante-huit foyers types ;
  moyennes de la consommation et des services publics lues sur des pages
  officielles (Insee, Douane, DEPP, Caf) ; statut
  « vérifié en partie » (voir les écarts et hypothèses plus haut).

## Données : ce qui reste reconstitué ou à contrôler
Dépenses de l'État par mission, branches et recettes de la Sécurité sociale,
ventilation des collectivités, séries 2007-2019, indicateurs retraites,
composition de la dette, textes de contexte, coût de la plupart des mesures,
hypothèses du simulateur budgétaire.
- Prélèvement UE 2026 : 28,8 Md€ est le montant du projet de loi de finances ;
  le montant de la loi promulguée n'a pas été recontrôlé.
- Contribution à l'UE 2007-2018 : non recontrôlée.
- Écart entre 37,4 et 40,3 Md€ du plan de relance attribué à REPowerEU :
  lecture de l'outil, non confirmée par une source.
- Incohérence connue : la dépense publique 2024 vaut 57,0 % du PIB dans
  « Où va l'argent » (PIB Eurostat d'octobre 2026) et 57,3 % dans la
  comparaison par fonction de l'onglet Europe (tableau Eurostat établi avec un
  PIB antérieur). À harmoniser (question posée, sans réponse à ce jour).
- Simulateur personnel : gel du SMIC lu sur service-public.gouv.fr et taux
  moyen d'accidents du travail lu sur le site du Cleiss, pas dans le décret ni
  l'arrêté eux-mêmes ; lecture de l'outil, non confirmée par une source : la
  contribution de l'État employeur aux pensions « équilibre le régime » ;
  reconduction
  de la contribution différentielle sur les hauts revenus pour 2026 non
  vérifiée (sans effet pour des salariés).

## API et accès réseau
- Domaines à autoriser : ec.europa.eu, data.ofgl.fr, www.insee.fr,
  api.insee.fr, data.economie.gouv.fr, www.data.gouv.fr, static.data.gouv.fr,
  webstat.banque-france.fr.
- API disponibles : OFGL, Eurostat (gov_10dd_edpt1, gov_10a_main, gov_10a_exp,
  nama_10_gdp, demo_gind).
- OpenFisca-France, API publique (https://api.fr.openfisca.org/latest/) :
  utilisée seulement à la préparation (barèmes et cas types), jamais par
  l'application.
- Le site de la Commission (commission.europa.eu) et celui de l'Assemblée
  nationale refusent les téléchargements automatiques de fichiers : les
  déposer à la main dans le dossier.

## Chantier en cours et feuille de route

Les trois ajouts décidés le 2 octobre 2026 sont livrés : flux France ↔ UE ;
vue détaillée « Où va l'argent » ; simulateur personnel « Mon bilan » (quatre
étapes, puis reprise des défauts mineurs le 4 octobre 2026).

Feuille de route demandée par Jonathan le 4 octobre 2026, dans cet ordre :
0. « Mon bilan » : projection jusqu'à la retraite et au-delà. Livrée le
   4 octobre 2026 (voir plus haut) ; deux écarts au cahier des charges et une
   question sur la garde attendent l'avis de Jonathan.
1. Budget 2027 : ajouter les données de la version initiale proposée par le
   gouvernement, en rendant la version visible à l'écran. Ensuite, sur
   demande : la version soumise au vote, puis la version adoptée, pour voir
   ce que change le débat parlementaire. Même chose pour 2025 et 2026.
   Document déjà dans le projet : « Plafonds de dépenses PLF 27.pdf ».
2. Refonte de l'ergonomie du site : regrouper dans une catégorie à part tous
   les simulateurs fondés sur des hypothèses et sur les saisies de
   l'utilisateur (« Mon bilan », « Simulateur »).
3. Refonte de l'interface avec le modèle de design « Steep » (dans les
   artefacts de Jonathan).
4. Seconde version du simulateur personnel : chômage, RSA, aides au logement,
   indépendant au réel, revenus du patrimoine.

## Autres pistes
- Séries complètes via API (Eurostat historique, OFGL, Insee base 2020 depuis 2007).
- Détail territorial (cartes régions, départements, communes).
- Vérifier les dépenses par mission (lois de règlement) et par branche.
- Liens partageables vers une vue, export image ou CSV, mode pédagogique guidé.
- Passe d'accessibilité complète (lecteurs d'écran) : le focus après dépliage
  est traité dans « Mon bilan » et « Où va l'argent ».

## Outils conservés dans le projet (claude/outils/)
- ue-flux-extraction.py, ova-extraction.py : régénèrent les blocs de données
  UEF et OVA (à relancer quand une nouvelle année est publiée).
- ue-flux-controle.py, ova-controle.py : contrôles indépendants des données.
- bilan-parametres.py : régénère le bloc BIL_P (barèmes) depuis OpenFisca et
  les valeurs saisies à la main avec leur source (lignes « MANUEL » à relire
  chaque année). bilan-oracle.py : recalcule les cas types avec OpenFisca et
  écrit bilan-cas-types.json (étape 1), bilan-cas-famille.json (étape 2,
  option --famille) et bilan-cas-situations.json (étape 3, option
  --situations), que les tests relisent sans réseau ; option --annoter :
  renseigne les écarts connus dans les fichiers de cas, sans appel au modèle.
- ue-flux-tests.mjs, ova-tests.mjs, bilan-tests.mjs, bilan-famille-tests.mjs,
  bilan-situations-tests.mjs, bilan-reste-tests.mjs, bilan-mineurs-tests.mjs,
  bilan-projection-tests.mjs, tests-helpers.mjs : 321 tests automatisés (Node
  + Playwright 1.56 + chart.js 4.4.1 en local ; lancer
  `node --test tests/*.test.mjs`, les fichiers de test dans un dossier tests/
  à côté de index.html, renommés ue-flux.test.mjs, ova.test.mjs,
  bilan.test.mjs, bilan-famille.test.mjs, bilan-situations.test.mjs,
  bilan-reste.test.mjs, bilan-mineurs.test.mjs, bilan-projection.test.mjs et
  helpers.mjs, avec les trois fichiers de cas types à côté).

## Préférences de travail
- Échanges en français ; chiffres toujours sourcés avec un niveau de fiabilité.
- Signaler clairement ce qui est vérifié et ce qui ne l'est pas.
- Conception validée avant tout développement ; tests écrits avant le code.
- Après chaque dépôt dans le dossier, relire le fichier déposé et le comparer
  à l'original (un dépôt a déjà écrit une ancienne version sans le signaler).
- Ne jamais citer une adresse de source écrite de mémoire : l'ouvrir d'abord
  (un lien inventé a été trouvé par la relecture de l'étape 2).
- Faire relire chaque étape par un relecteur indépendant avant de livrer : il
  a trouvé des erreurs réelles aux quatre étapes.
- Quand une recherche de sources est déléguée, rouvrir soi-même les pages
  dont les chiffres entrent dans l'application avant de les citer.
- Les pages web sont lues par un outil qui les résume : il a rendu deux
  « citations exactes » différentes pour la même page. Reprendre les valeurs
  et les dates, jamais des mots entre guillemets ; écrire « lecture de
  l'outil » quand une phrase va au-delà de ce que la page établit.
- Avant de choisir les couleurs d'un graphique, les passer au validateur de
  palette : les couleurs actuelles de l'application ne fournissent que deux
  teintes sûres ensemble (bleu « État » et ocre « collectivités ») ; à
  reprendre avec la refonte « Steep ».
