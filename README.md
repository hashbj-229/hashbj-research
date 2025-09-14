# hashbj-research
Avec les avancées technologiques actuelles, pourrait-on créer une
cryptographie infaillible ?

*Rédigé par : Welman GBAGUIDI, Hector SEDO, Destin ATCHAHOUE*

------------------------------------------------------------------------

## Résumé

La cryptographie contemporaine évolue entre deux réalités : la sécurité
inconditionnelle (garantie théorique) et la sécurité computationnelle
(basée sur des hypothèses de complexité). Mais à l'ère du calcul
quantique et de l'intelligence artificielle, ce fragile équilibre est
remis en question. L'algorithme de Shor menace directement RSA et ECC,
tandis que des attaques pratiques --- comme celles par canaux
auxiliaires, les failles matérielles, ou encore les erreurs humaines ---
montrent que la vulnérabilité dépasse largement le cadre purement
mathématique.

Dans ce travail, nous présentons :

Les modèles de sécurité (informationnelle, computationnelle, quantique).
Les menaces émergentes, notamment la stratégie « store now, decrypt
later ». L'état de la cryptographie post-quantique (PQC) et de la
cryptographie quantique (QKD). Une feuille de route pragmatique qui
privilégie la gestion du risque et la crypto-agilité plutôt qu'une quête
illusoire d'infaillibilité.

------------------------------------------------------------------------

## 1. Introduction et problématique

La cryptographie n'est plus réservée aux experts : elle est devenue un
pilier de nos sociétés modernes, régissant les paiements en ligne, les
télécommunications, la santé, et même la gouvernance numérique.

La question « Peut-on créer une cryptographie infaillible ? » doit être
scindée en deux :

*Théorie pure* : existe-t-il un schéma incassable, quelles que soient
les ressources de l'adversaire ? *Pratique* : peut-on garantir
l'inviolabilité d'un système complet (algorithmes, implémentations,
matériel, facteurs humains) ?

Réponse synthétique :

Oui pour la théorie (l'OTP de Shannon), mais avec des contraintes
logistiques insurmontables. Non dans la pratique, car tout système réel
repose sur une chaîne de maillons vulnérables.

------------------------------------------------------------------------

## 2. Modèles de sécurité

### 2.1 Sécurité informationnelle

un schéma est informationnellement sûr si l’observation du texte chiffré 
𝐶
C donne aucune information sur le message 
𝑀
M — en probabilités conditionnelles : 
𝑃
(
𝑀
∣
𝐶
)
=
𝑃
(
𝑀
)
P(M∣C)=P(M). Shannon a formalisé ce concept et a prouvé que le One-Time Pad (OTP) réalise la sécurité parfaite sous conditions strictes (clé aléatoire de longueur ≥ message, utilisée une seule fois, parfaitement secrète). 
pages.cs.wisc.edu

Conséquence formelle (Shannon) : l’existence d’un chiffrement à parfaite sécurité impose une clé d’entropie au moins égale à celle du message — d’où l’impraticabilité à grande échelle.

### 2.2 Sécurité computationnelle

Définition : un schéma est sécurisé computationnellement si toute attaque efficace (temps polynomial, ressources réalistes) est supposée inenvisageable — mais cela dépend d’hypothèses (par ex. difficulté de factorisation ou du logarithme discret). La sécurité est exprimée via des notions standard : IND-CPA (indistinguishability under chosen-plaintext attack), IND-CCA (chosen-ciphertext), preuves de réduction (réduction de la réussite d’un attaquant à la résolution d’un problème mathématique supposé dur).

### 2.3 Adversaire quantique

Un adversaire quantique dispose d’un ordinateur quantique et, le cas échéant, d’un accès quantique aux oracles (modèle « QROM » — Quantum Random Oracle Model). Les algorithmes quantiques (Shor, Grover) perturbent les hypothèses de sécurité : Shor détruit la difficulté de factorisation/log-discret, Grover réduit la sécurité d’un facteur ≈ √ pour les recherches non structurées.

L’idéal inconditionnel : le One-Time Pad (OTP) et ses limites pratiques

------------------------------------------------------------------------

## 3. L'idéal théorique : OTP et ses limites

OTP : chiffrement bit à bit 
𝐶
=
𝑀
⊕
𝐾
C=M⊕K avec clé 
𝐾
K uniformément aléatoire et 
∣
𝐾
∣
≥
∣
𝑀
∣
∣K∣≥∣M∣. Shannon a montré que l’entropie de 
𝐾
K doit être au moins celle de 
𝑀
M pour obtenir la parfaite sécurité. Toute réutilisation de 
𝐾
K brise la sécurité (ex. Venona). 
pages.cs.wisc.edu
+1

## 3.1 Cas historique : Venona

Le projet Venona (USA) a exploité la réutilisation partielle des masques jetables soviétiques pour récupérer des communications, démontrant qu’un seul manquement opérationnel annule la sécurité théorique. 
Agence de sécurité nationale

## 3.2 Pourquoi OTP n’est pas une solution pratique à grande échelle

Distribution secure de clés aussi longues que les messages (coût/latence/entropie réelle).

Stockage et protection des clés: surface d’attaque grande.

Contraintes de synchronisation et d’erreurs.
Conclusion : OTP demeure un outil de niche (cas où la logistique est maîtrisée), pas une solution universelle.

------------------------------------------------------------------------


## 4 Fondations mathématiques courantes

RSA ⟺ factorisation entière.

ECC ⟺ problème du logarithme discret sur courbes elliptiques.

AES / algorithmes symétriques ⟺ sécurité pratique par recherche exhaustive (ou structure interne résistante aux attaques analytiques).

Ces systèmes reposent sur des conjectures non prouvées (P ≠ NP et autres hypothèses de difficulté). Une preuve que 
𝑃
=
𝑁
𝑃
P=NP ou une découverte mathématique majeure bouleverserait l’écosystème. (Ce risque est théorique mais conceptuellement critique.)

## 4.1 Algorithmes quantiques — conséquences directes

Shor (1994) : algorithme polynomial pour factorisation et logarithme discret — rendrait RSA/ECC vulnérables en temps polynomial sur un ordinateur quantique universel suffisamment grand. 
epubs.siam.org

Grover (1996) : donne un gain quadratique pour recherche non structurée (impact sur clés symétriques : sécurité effective ≈ racine carrée de l’espace de clés, exigeant l’allongement des clés symétriques). 
arXiv

## 4.2 Horizon temporel du « Q-day » (critiques et incertitudes)

Estimer la date où un ordinateur quantique cryptanalytiquement pertinent (CRQC) existera est incertain. Des sondages d’experts et des études de la filière placent la probabilité significative d’un CRQC dans les années 2030 (milieu → fin 2030s) ; d’autres travaux (optimisations d’algorithmes et progrès matériels) font varier l’estimation sensiblement. L’idée stratégique "store now, decrypt later" est reconnue par NIST comme un vecteur d’attaque plausible (collecte aujourd’hui, déchiffrement demain). 
NIST
+1

Note : des résultats de recherche récents peuvent réduire le nombre de qubits nécessaires (voir travaux de 2024–2025) — cela accélère la chronologie potentielle et renforce l’urgence de préparations pragmatiques. 
The Quantum Insider

Cryptographie post-quantique (PQC) : familles, état de la normalisation et limites


------------------------------------------------------------------------

## 5 Familles principales et intuition cryptographique

Lattice-based (réseaux) : LWE, Ring-LWE → primitives performantes, bases de preuves pour sécurité et constructions avancées (ex. chiffrement, signatures, HHE).

Hash-based : signatures immuables fondées sur la résistance des fonctions de hachage (ex. SPHINCS+).

Code-based : McEliece et variantes — solides mais avec tailles de clé souvent grandes.

Multivariate : signatures basées sur systèmes multivariés (fragile selon variantes).

Isogeny-based : SIKE (isogénies) offrait de petites clés mais a été attaqué.

Ces familles répondent à des hypothèses mathématiques différentes — la diversification réduit le risque qu’une faille unique fasse tomber l’ensemble. 
pages.cs.wisc.edu

## 5.1 Normalisation NIST et statut (rétrospective)

Le NIST a piloté un processus de normalisation depuis 2016 et a sélectionné des candidats finaux. Les principaux algorithmes choisis pour normalisation (chiffrement/KEM et signatures) comprennent CRYSTALS-Kyber, CRYSTALS-Dilithium, Falcon, SPHINCS+, avec documents et spécifications publiés par le NIST. L’effort de normalisation est en cours d’intégration dans standards gouvernementaux et industriels. 
NIST
+1

## 5.2 Attaques et maturité : prudence nécessaire

Plusieurs algorithmes finalistes ont été cassés (ou fortement révisés) lors de l’évaluation cryptanalytique (ex. SIKE a subi une attaque efficace — Castryck-Decru). Ceci illustre que réussir la normalisation ne garantit pas l’immuabilité : toute proposition doit traverser des années d’analyse. 
math.mit.edu
+1

## 5.3 Contraintes pratiques de la PQC

Tailles de clés / signatures : certains schémas augmentent significativement les données transmises — problèmes pour IoT/embedded.

Performance & compatibilité : intégration dans TLS/PKI/firmware exige tests et ajustements.

Crypto-agilité : nécessité d’architectures permettant migration progressive (hybridation, mises à jour rapides). 
csrc.nist.gov

Cryptographie quantique (QKD) : promesses et limites pratiques

QKD promet une distribution de clé avec sécurité physique (détection d’interception); cependant : portée limitée, coût élevé, intégration complexe dans réseaux existants, et vulnérabilités de mise en œuvre (atténuations, attaques sur composants). En pratique, QKD est utile pour certains cas d’usage hautement sensibles, mais ne constitue pas aujourd’hui une solution universelle. (Voir évaluations nationales et études d’agences comme l’ANSSI.) 
pages.cs.wisc.edu
+1

Le talon d’Achille : vulnérabilités pratiques et humaines (études de cas)

------------------------------------------------------------------------

## 6. Cryptographie quantique (QKD)

La QKD promet une distribution de clés inviolable, mais souffre de :

Coûts élevés. Portée limitée. Vulnérabilités d'implémentation.

Utilité : seulement pour des contextes ultra-sensibles (gouvernements,
défense).

------------------------------------------------------------------------

## 7 Attaques par canaux auxiliaires (side-channel)

Les attaques par temps d’exécution, consommation électrique, émissions électromagnétiques, et even acoustique extraient des secrets d’implémentations réelles. Paul Kocher et al. ont documenté les attaques de timing et de Differential Power Analysis (DPA) qui, en pratique, forcent des modifications d’implémentation et des contre-mesures matérielles. 
paulkocher.com
+1

Exemple technique : une implémentation RSA qui ne masque pas les opérations multiplicatives peut révéler bits de la clé via corrélation entre consommation et opérations; des techniques de masquage/blinding et d’exécution constante sont nécessaires.

## 7.1 Failles matérielles de grande ampleur — Meltdown & Spectre

Ces vulnérabilités microarchitecturales (exécution spéculative, prédiction de branchement) ont permis l’exfiltration de données sensibles en mémoire, démontrant que la sécurité peut être compromise à des couches inattendues (CPU). Les correctifs sont coûteux et certains remèdes impliquent un compromis performance/sécurité. 
spectreattack.com
+1

## 7.2 Erreurs d’implémentation et vulnérabilités industrielles — ROCA

La vulnérabilité ROCA (2017) montre qu’une mauvaise implémentation de génération de clés dans une bibliothèque matérielle (Infineon RSALib) a produit des clés RSA vulnérables malgré l’algorithme mathématiquement sûr. La leçon : l’analyse de la chaîne d’implémentation est cruciale. 
ncsc.gov.uk
+1

## 7.3 Facteur humain et gouvernance (PKI, mots de passe, procédures)

Les attaques d’ingénierie sociale, la mauvaise gestion de certificats et la fragmentation des opérations cryptographiques en entreprise multiplient les risques : ENISA et autres agences insistent sur l’inventaire et la centralisation de la gestion des clés.

Analyses quantitatives et scénarios (approche raisonnable)

------------------------------------------------------------------------

## 8.Analyses et Scénarios

Un des scénarios critiques à anticiper pour les systèmes utilisant RSA-2048 (et d’autres primitives sensibles) est la maturation des ordinateurs quantiques jusqu’à pouvoir exécuter l’algorithme de Shor de façon fonctionnelle et fiable. Actuellement, bien que Shor soit théoriquement capable de casser RSA-2048 en temps polynomial, les ressources réelles requises restent énormes, rendant cette menace pertinente, mais non immédiate. Plusieurs publications récentes clarifient ces contraintes techniques et les implications pour la migration vers la cryptographie post-quantique (PQC).

## 8.1 Capacité actuelle et ressources requises pour Shor sur RSA-2048

Une estimation notable (Gidney & Ekerå, 2021) indique qu’il faudrait environ 6 190 qubits logiques pour casser RSA-2048 en un jour, dans des conditions de bruit limité (taux d'erreur ~10⁻³) et avec une cadence de surface cycle (quantum clock) de 200 ns. 
Kudelski Security Research

Une autre estimation publiée dans PostQuantum.com mentionne qu’environ 20 millions de qubits physiques pourraient suffire à casser RSA-2048 en 8 heures, si l’on assume des qubits avec correction d'erreur (noisy qubits) et une architecture qui permet cette durée de cohérence. 
PostQuantum.com
+1

Une avancée plus récente (Chevignard et al., 2024) propose une réduction du nombre de qubits logiques nécessaires à environ 1 730 pour un module RSA-2048 en utilisant des optimisations importantes, mais cela s’accompagne d’un circuit très profond, d’un nombre élevé de portes Toffoli, et d’un grand nombre d’exécutions (répétitions), ce qui ralentit énormément le temps total. 
PostQuantum.com
+1

Ces données montrent que, bien que l’on fasse des progrès, la construction d’un ordinateur quantique capable d’exécuter Shor sur RSA-2048 dans un délai opérationnel (quelques heures) reste hors de portée pour le moment.

## 8.2 Scénarios de migration vers la PQC basés sur la durée de confidentialité des données

Compte tenu des délais estimés pour la maturité quantique, les organisations doivent planifier leur migration vers des algorithmes résistants aux attaques quantiques selon la durée pendant laquelle les données doivent rester confidentielles.

Scénario “Durée de confidentialité > 10 ans” :
Si les données doivent rester sécurisées pendant plus de dix ans (par exemple données légales, médicales, archivage institutionnel), alors la migration vers PQC doit être entreprise immédiatement. Ceci pour éviter qu’elles soient capturables dans le futur ou stockées aujourd’hui avec la perspective d’être brisées plus tard (risque “harvest-now, decrypt-later”).

Scénario “Durée de confidentialité < 5 ans” :
Pour des données dont l’importance diminue rapidement dans le temps (ex. certaines communications internes, logs temporaires, données à usage immédiat), une transition graduelle est possible. On peut garder les primitives classiques en usage maintenant, tout en planifiant des étapes de migration (inventaire des usages, tests PQC, mise à jour des protocoles) pour quand les composants PQC matures sont disponibles.

Scénario intermédiaire (entre 5 et 10 ans) :
Dans ce cas, une stratégie hybride est recommandée: déploiement simultané de versions PQC dans les systèmes critiques, migration partielle progressive, et maintien des algorithmes classiques avec réserves (back-compatibilité, vérification des risques). Les organisations doivent faire des évaluations de risque, chiffrer les données sensibles dès maintenant, et stocker les données critiques selon des algorithmes déjà quant-safe ou double protection (chiffrement classique + PQC).

## 8.3 Implications techniques pour les infrastructures critiques

Audit cryptographique : il faut inventorier tous les usages de crypto (chiffrement, signatures, certificats, hachage) pour identifier les points sensibles qui pourraient être compromis demain par une attaque quantique.

Compatibilité des systèmes existants : certaines infrastructures matérielles/logiciels anciens ne supporteront pas facilement les nouveaux algorithmes (PQC) à cause des contraintes de performance, de latence, de taille des clés, ou encore exigences de puissance de calcul.

Surveillance cryptanalytique continue : les avancées comme celles de Chevignard montrent que les estimations de ressources pour Shor évoluent rapidement. Ce qui était jugé impossible ou lointain peut devenir proche. Il faut suivre les publications, prototypes, et les progrès matériels.

Planification stratégique : établir un calendrier dirigé par la criticité des données, décider des priorités (quel service/mquelle infrastructure migrer en premier), tester les algorithmes PQC, former les équipes, prévoir le coût de remplacement ou de mise à niveau.

## 8.4 Synthèse de la partie

Les scénarios montrent que bien qu’un Shor pleinement fonctionnel sur RSA-2048 ne soit pas immédiat, les estimations convergent vers un horizon technique sérieux : des milliers à des millions de qubits (physiques ou logiques) avec correction d’erreur, des circuits profonds, temps de calcul élevé, etc. En fonction de la durée pendant laquelle les données doivent rester confidentielles, la migration vers la cryptographie post-quantique ne peut plus être perçue comme une option lointaine, mais comme une exigence à planifier dès maintenant. Les organisations qui ignorent ces signaux s’exposent au risque que des données sensibles d’aujourd’hui deviennent vulnérables demain.

------------------------------------------------------------------------

## 9. Feuille de route pragmatique

L’intégration de la cryptographie post-quantique (PQC) et l’ajustement des systèmes de protection aux menaces émergentes ne sauraient se réduire à un simple geste technique. Cela requiert une démarche ordonnée, tangible et progressive, où se croisent visions stratégiques, structures organisationnelles et architectures technologiques.

La première marche consiste à dresser une véritable cartographie du patrimoine cryptographique. Chaque entité doit procéder à un inventaire minutieux des algorithmes, protocoles et bibliothèques employés, qu’il s’agisse de certificats, de services en nuage, de modules matériels ou d’applications vitales. Cette radiographie dévoile les fragilités majeures et permet de jauger l’exposition au péril du harvest now, decrypt later.

Vient ensuite la hiérarchisation des données selon leur durée de vie. Les informations dont la confidentialité doit survivre plusieurs décennies — archives médicales, dossiers juridiques, secrets industriels ou communications d’État — doivent impérativement migrer vers des schémas de chiffrement conçus pour contrer la puissance quantique. Les données de valeur temporelle limitée, en revanche, peuvent s’inscrire dans une migration progressive et modulée.

L’érection d’une véritable crypto-agilité constitue l’un des piliers de cette transformation. L’idée est de bâtir des systèmes polymorphes, capables de supporter en parallèle des algorithmes classiques et post-quantiques, et d’opérer un basculement fluide en fonction de l’évolution des normes et du spectre des menaces. Cette hybridation PQC + classique est, de surcroît, plébiscitée par le NIST et l’ETSI comme passage intermédiaire incontournable.

Simultanément, une gouvernance rigoureuse et une culture de méfiance absolue — le Zéro-Trust — doivent être instaurées. Cela suppose des contrôles continus, une séparation hermétique des privilèges, une rotation disciplinée des clés ainsi qu’une vérification incessante des identités et des accès. Sans cette charpente de sécurité intégrée, auditée et adaptée aux réalités opérationnelles, la cryptographie ne saurait atteindre son plein potentiel.

Enfin, il est vital de consolider la robustesse face aux assauts physiques et logiciels. Trop souvent, ce ne sont pas les algorithmes en eux-mêmes qui cèdent, mais leurs implémentations : vulnérabilités logicielles, failles matérielles, attaques par canaux auxiliaires. L’ajout de contre-mesures sophistiquées — obfuscation, randomisation temporelle, défenses matérielles anti-side-channel — devient alors un pilier de la résilience.

En somme, la route vers une sécurité post-quantique ne s’improvise pas : elle se trace comme une architecture vivante, enracinée dans la stratégie, pétrie d’agilité et bardée de contre-feux face aux tempêtes numériques de demain.

------------------------------------------------------------------------

## 10 – Études de cas en cryptographie : Exploration technique

L’odyssée de la cryptographie moderne n’est pas pavée uniquement de triomphes éclatants, mais aussi de fissures inattendues découvertes au cœur de systèmes que l’on croyait infranchissables. Chacune de ces brèches, étudiée à la loupe, révèle une vérité essentielle : même les forteresses algorithmiques les plus réputées peuvent être fragilisées par une implémentation négligente, une hypothèse mathématique trop candide ou une discipline défaillante dans la gestion des clés. Trois affaires emblématiques illustrent magistralement ces limites.

## 10.1 Venona : quand le One-Time Pad s’effondre sous la réutilisation de clés

Principe en jeu : sécurité absolue du One-Time Pad (OTP).
Observation technique : L’OTP repose sur un axiome implacable : chaque clé doit être aléatoire, unique et équivalente en longueur au message. Mais dans le projet Venona, des clés furent réutilisées, créant ainsi des motifs exploitables.
Conséquence : Les cryptanalystes parvinrent à déchiffrer des communications censées demeurer impénétrables. Une simple maladresse humaine dans la gestion des clés anéantit ce que l’on considérait comme une perfection mathématique.
Enseignement : La robustesse cryptographique ne se joue pas uniquement sur l’épure algébrique ; elle exige une rigueur quasi militaire dans l’implémentation et la distribution des clés (Stinnett, 2017).

## 10.2 ROCA : l’érosion de RSA par une implémentation matérielle viciée

Principe en jeu : solidité de RSA, reposant sur la difficulté de factoriser de grands entiers.
Observation technique : La bibliothèque Infineon RSALib produisait des clés avec une structure prévisible. Cette faille ouvrit la porte à une attaque de type Coppersmith, ramenant la complexité de la factorisation à une dimension accessible.
Conséquence : Des millions de cartes d’identité électroniques et modules TPM furent mis à nu, sapant la confiance placée dans une infrastructure sécuritaire à l’échelle mondiale.
Enseignement : Un algorithme impeccable sur le plan théorique peut sombrer à cause d’une implémentation boiteuse. Les audits cryptographiques, tant logiciels que matériels, deviennent ainsi incontournables (ROCA Advisory, 2017).

## 10.3 SIKE : l’échec brutal d’un prétendant post-quantique

Principe en jeu : sécurité post-quantique fondée sur les isogénies supersingulières.
Observation technique : En 2022, une attaque classique réduisit SIKEp434 en poussière en moins d’une heure, exposant des raccourcis structurels exploitables.
Conséquence : L’un des candidats phares du programme NIST PQC fut écarté, démontrant que même des schémas conçus pour résister aux ordinateurs quantiques peuvent succomber devant une attaque classique bien ourdie.
Enseignement : La validation d’algorithmes post-quantiques requiert une cryptanalyse exhaustive, conjuguant perspectives classiques et quantiques (Schneier, 2022).

Synthèse

Venona, ROCA et SIKE incarnent une leçon intemporelle : la cryptographie n’est pas qu’un exercice mathématique abstrait, mais une discipline où la praxis importe autant que la théorie. La sécurité opérationnelle repose sur trois piliers indissociables :

une gouvernance irréprochable des clés,

des implémentations matérielles et logicielles rigoureusement auditées,

une vigilance constante face aux progrès cryptanalytiques.

Dans cet univers, la moindre entorse à un principe cardinal — réutilisation de clés, bibliothèque vulnérable ou choix algébrique fragile — suffit à transformer une citadelle supposément invincible en un bastion fracturé.

------------------------------------------------------------------------

## 11. Discussion

Le One-Time Pad (OTP) est le seul système de cryptographie qui est
théoriquement inviolable. La sécurité est totale si la clé est
aléatoire, unique et au moins aussi longue que le message. En pratique,
aucun système utilisé à grande échelle n'est parfait. Les failles
viennent surtout des utilisateurs, des logiciels ou du matériel.

Les nouvelles technologies changent un peu les règles : la cryptographie
post-quantique (PQC) protège contre les ordinateurs quantiques, mais
elle demande des ressources importantes et une surveillance constante.
La Quantum Key Distribution (QKD) permet d'échanger des clés de manière
très sûre, mais seulement dans des situations limitées. Même avec ces
techniques, aucun système réel n'est complètement inviolable. La
sécurité dépend toujours de la bonne mise en œuvre, de la gestion des
clés et d'une surveillance régulière (Shannon, 1949 , NIST PQC Project

## 12- Perspectives et Prévisions

À l'avenir, la cryptographie pourrait évoluer vers des systèmes hybrides
combinant sécurité parfaite et probabilité, intégrant des technologies
telles que la cryptographie quantique et l'IA. La collaboration
internationale et l'investissement dans la recherche locale seront
cruciaux pour développer des solutions adaptées aux défis émergents.

## 13. Conclusion

La cryptographie infaillible est une *utopie* pour les usages réels.
L'approche réaliste est systémique :

Diversification mathématique (PQC). Hygiène d'implémentation (résistance
aux side-channels). Gouvernance centralisée des clés. Crypto-agilité
pour anticiper les ruptures technologiques. Formation continue des
acteurs.

En somme, la sécurité n'est pas un état figé, mais un *processus vivant
et adaptatif*.

------------------------------------------------------------------------

## Références principales

C. Shannon, Communication Theory of Secrecy Systems, 1949. P. Shor,
Polynomial-Time Algorithms for Prime Factorization and Discrete
Logarithms on a Quantum Computer, 1994. L. Grover, A fast quantum
mechanical algorithm for database search, 1996. NIST, Post-Quantum
Cryptography Project, 2016--2024. Castryck & Decru, Attack on SIKE,
2022. P. Kocher, Timing Attacks on Implementations of Diffie-Hellman,
RSA, DSS..., CRYPTO 1996. NCSC, ROCA Vulnerability Report, 2017. Spectre
& Meltdown disclosures, 2018. NIST Post-Quantum Cryptography project ---
Selected algorithms and announcements (2016--2024) Castryck & Decru,
Attack on SIKE / isogeny (exposés et notes), 2022. math.mit.edu Paul C.
Kocher, Timing Attacks on Implementations of Diffie-Hellman, RSA, DSS,
and Other Systems, CRYPTO 1996. paulkocher.com

Paul C. Kocher, Jaffe, Jun, Differential Power Analysis, CRYPTO 1999.
paulkocher.com 10:40 intervention de l'ia dans l domaine de la
cryptographie apport et impact 10:41 Arnon-Friedman, R., Renner, R., &
Vidick, T. (2016). Simple and tight device-independent security proofs.
arXiv.

Kuang, R., & Bettenburg, N. (2023). Shannon Perfect Secrecy in a
Discrete Hilbert Space. arXiv.

Wikipédia. (n.d.). Cryptographie asymétrique. Consulté le 14 septembre
2025, sur https://fr.wikipedia.org/wiki/Cryptographie_asym%C3%A9trique
