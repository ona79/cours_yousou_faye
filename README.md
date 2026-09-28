# Documentation Technique — SEC.NET
## Cours Interactif de Sécurité des Réseaux

**Auteur du cours** : Pr. Youssou FAYE  
**TP encadrés par** : Dr. Malaw NDIAYE  
**Institution** : Université Assane Seck de Ziguinchor (UASZ)  
**UFR** : Sciences & Technologies — Département Informatique  
**Niveau** : Licence 3 Ingénierie Informatique  
**Année académique** : 2025-2026  

---

## Table des matières

1. [Présentation générale](#1-présentation-générale)
2. [Architecture du projet](#2-architecture-du-projet)
3. [Stack technologique et dépendances](#3-stack-technologique-et-dépendances)
4. [Système de design (CSS)](#4-système-de-design-css)
5. [Composants réutilisables](#5-composants-réutilisables)
6. [Navigation et routing](#6-navigation-et-routing)
7. [Contenu pédagogique](#7-contenu-pédagogique)
8. [Système de quiz interactif](#8-système-de-quiz-interactif)
9. [JavaScript — fonctionnalités](#9-javascript--fonctionnalités)
10. [Responsive design](#10-responsive-design)
11. [SEO et accessibilité](#11-seo-et-accessibilité)
12. [Guide de contribution](#12-guide-de-contribution)
13. [Roadmap — Chapitres futurs](#13-roadmap--chapitres-futurs)
14. [Annexes](#14-annexes)

---

## 1. Présentation générale

**SEC.NET** est une application web éducative monofichier (`index.html`, environ 199 Ko, 3 580 lignes) conçue pour présenter de manière interactive le cours de **Sécurité des Réseaux** dispensé en L3 Ingénierie Informatique à l'UASZ.

### Objectifs pédagogiques

| Objectif | Description |
|---|---|
| Cours | Présenter les fondements théoriques de la cybersécurité |
| TD | Proposer des exercices de cryptographie et protocoles |
| TP | Guider les manipulations pratiques (OpenSSL, Wireshark, Squid) |
| Quiz | Évaluer la compréhension via 29 questions interactives |

### Points forts

- Monofichier : aucune dépendance locale, fonctionne sans serveur web
- Responsive : adapté mobile, tablette et desktop
- Interactif : cube 3D CSS, matrice cliquable, accordéons, notifications toast, quiz avec score
- Thème dark mode avec effets glow, scanlines et particules flottantes

---

## 2. Architecture du projet

```
secu/
├── index.html          # Application complète (HTML + CSS + JS)
└── README.md           # Documentation du projet
```

### Structure interne de `index.html`

```
<head>
  ├── Meta (charset, viewport, title)
  ├── Tailwind CSS CDN
  ├── Google Fonts (Space Grotesk, JetBrains Mono, Syncopate)
  ├── Font Awesome 6.4
  └── <style> — Design system custom (~470 lignes CSS)

<body>
  ├── #toast                    Notification flottante globale
  ├── #particles                Particules animées d'arrière-plan (JS)
  ├── <nav>                     Barre de navigation fixe
  │   ├── Logo SEC.NET
  │   ├── Menu desktop avec dropdowns imbriqués
  │   ├── Bouton "START QUIZ"
  │   └── Bouton menu burger (mobile)
  ├── #mobileMenu               Menu mobile plein écran
  ├── <header>                  Section hero
  ├── Section plan du cours     Grille de 6 cartes chapitres
  ├── #intro                    Chapitre 01 : Définitions
  ├── #cyber                    Cybersécurité
  ├── #hackers                  Pirates vs Hackers
  ├── Section approche trad.    Prévention / Détection / Réaction
  ├── #risques                  Risques / Vulnérabilités / Menaces
  ├── #matrice                  Matrice interactive des risques
  ├── #iso                      ISO/IEC 27005 et PDCA
  ├── #cid                      Triade CID
  ├── #cube                     Cube de McCumber (3D CSS animé)
  ├── #crypto                   Chapitre 03 : Cryptographie (accordéons)
  ├── #td                       Travaux Dirigés TD1–TD4
  ├── #tp                       Travaux Pratiques TP1–TP4
  ├── #quiz                     Quiz interactif 29 questions
  ├── <footer>                  Informations institutionnelles
  └── <script>                  Logique JavaScript (~490 lignes)
```

---

## 3. Stack technologique et dépendances

| Technologie | Version | Rôle | Source |
|---|---|---|---|
| HTML5 | — | Structure sémantique | Natif |
| Tailwind CSS | CDN latest | Classes utilitaires layout et espacement | `cdn.tailwindcss.com` |
| CSS Vanilla | — | Design system, animations, composants | Inline `<style>` |
| JavaScript ES6+ | — | Interactivité, quiz, animations | Inline `<script>` |
| Google Fonts | — | Space Grotesk, JetBrains Mono, Syncopate | `fonts.googleapis.com` |
| Font Awesome | 6.4.0 | Icônes | `cdnjs.cloudflare.com` |

Le projet nécessite une connexion Internet pour charger Tailwind CSS, Google Fonts et Font Awesome. Pour un déploiement hors ligne, ces ressources devront être hébergées localement.

---

## 4. Système de design (CSS)

### Variables CSS (`:root`)

```css
--bg       : #0f1621                    /* Fond principal — noir bleuté      */
--bg-2     : #161f2e                    /* Fond secondaire                   */
--fg       : #eef4ff                    /* Texte principal                   */
--muted    : #96a6c2                    /* Texte secondaire                  */
--accent   : #00ffea                    /* Cyan néon — couleur principale    */
--accent-2 : #00ff88                    /* Vert néon — couleur secondaire    */
--danger   : #ff3366                    /* Rouge danger                      */
--warning  : #ffb800                    /* Ambre avertissement               */
--card     : rgba(26,35,52,0.72)        /* Fond carte glassmorphism          */
--border   : rgba(0,255,234,0.18)       /* Bordure subtile cyan              */
```

### Typographies

| Classe | Police | Utilisation |
|---|---|---|
| `.font-display` | Syncopate | Titres principaux H1, H2 |
| `.font-mono` | JetBrains Mono | Labels, code, tags, navigation |
| Corps par défaut | Space Grotesk | Texte courant |

### Classes d'effets visuels

| Classe | Effet |
|---|---|
| `.bg-grid` | Grille de lignes cyan très subtile, maille 50×50 px |
| `.bg-radial` | Halos radials colorés (cyan, rouge, vert) en arrière-plan |
| `.scanline::before` | Lignes de scan style CRT via `linear-gradient` |
| `.glow-cyan` | `text-shadow` cyan lumineux à deux niveaux |
| `.glow-red` | `text-shadow` rouge lumineux |
| `.glow-green` | `text-shadow` vert lumineux |
| `.glitch:hover` | Animation de décalage rapide au survol |
| `.particle` | Particules flottantes injectées par JavaScript |

### Animations keyframes

| Nom | Description | Durée |
|---|---|---|
| `rotateCube` | Rotation 3D continue du cube McCumber | 25 s, infini |
| `pulse` | Pulsation du point de statut « en ligne » | 2 s, infini |
| `float` | Montée des particules d'arrière-plan | 6–12 s, infini |
| `glitch` | Micro-décalages pour effet de corruption visuelle | 0,3 s |

---

## 5. Composants réutilisables

### `.card`

Carte glassmorphism avec bordure lumineuse animée.

```css
background    : var(--card);          /* rgba avec opacité */
backdrop-filter: blur(10px);
border        : 1px solid var(--border);
border-radius : 14px;
transition    : all .4s cubic-bezier(.4,0,.2,1);
```

Au survol : remontée de 4 px, ombre cyan portée, bordure plus visible, et une ligne de lumière traverse la carte horizontalement via `::before`.

---

### `.btn-cyber`

Bouton style cyberpunk à remplissage glissant.

```css
background    : transparent;
border        : 1px solid var(--accent);
color         : var(--accent);
font-family   : JetBrains Mono;
text-transform: uppercase;
```

Au survol : le fond cyan glisse de gauche à droite via `::before translateX`, et le texte passe en noir.

---

### `.section-tag`

Label monospace compact, fond semi-transparent cyan, lettres très espacées. Utilisé comme indicateur de section ou de catégorie en haut de chaque bloc.

---

### `details.acc` — Accordéon

```css
border       : 1px solid var(--border);
border-radius: 12px;
background   : rgba(22,31,46,0.5);
```

Le `summary::after` affiche un `+` qui pivote à 45° à l'ouverture. Utilisé massivement dans les sections Cryptographie, TD et TP. La classe `.acc-sub` est une variante sans bordure pour les sous-niveaux du menu mobile.

---

### `.code-block` — Bloc de code / terminal

```css
background   : #0a0f18;
font-family  : JetBrains Mono;
font-size    : 12.5px;
color        : #8effea;
white-space  : pre-wrap;
word-break   : break-word;
```

La classe `.cmt` à l'intérieur colore les commentaires en gris `#6b7a94`.

---

### `.index-card` — Carte d'index TD/TP

Lien `<a>` stylisé en carte, bordure qui s'illumine au survol avec légère remontée et ombre portée. Utilisé dans les grilles d'index des sections TD et TP.

---

### `.quiz-option` — Option de quiz

Fond semi-transparent avec bordure, transitions de couleur automatiques selon l'action :

| État | Classe | Rendu |
|---|---|---|
| Survol | — | Bordure cyan, fond légèrement éclairé |
| Correct | `.correct` | Bordure et texte vert néon |
| Incorrect | `.wrong` | Bordure et texte rouge |
| Verrouillé | `.disabled` | `pointer-events: none`, opacité réduite |

---

### `.matrix-cell` — Cellule de la matrice des risques

Carré avec `aspect-ratio: 1`, quatre variantes de couleur :

| Classe | Couleur | Signification |
|---|---|---|
| `.matrix-green` | `#00ff88` | Tolérable |
| `.matrix-yellow` | `#ffb800` | Critique |
| `.matrix-orange` | `#ff6600` | Catastrophique (intermédiaire) |
| `.matrix-red` | `#ff3366` | Catastrophique maximal |

---

### `.toast` — Notification flottante

Position fixe en bas à droite. Slide-in depuis la droite sur desktop, slide-up depuis le bas sur mobile. Disparition automatique après 2 500 ms via `clearTimeout` + `setTimeout`.

---

## 6. Navigation et routing

### Menu desktop (largeur >= 768 px)

Navigation fixe (`position: fixed; top: 0`) avec dropdowns CSS purs au survol et un sous-menu déclenché au survol de la ligne parente.

```
ACCUEIL
PLAN DU COURS
  01  Introduction ................................. #intro
  02  Généralités sur la sécurité
        Cybersécurité .............................. #cyber
        Typologie des hackers ...................... #hackers
        Risques, menaces & vulnérabilités .......... #risques
        Matrice des risques ........................ #matrice
        Norme ISO/CEI 27005 ........................ #iso
        Triade CID ................................. #cid
        Cube de McCumber ........................... #cube
  03  La Cryptographie
        Introduction & définitions ................. #crypto-intro
        Cryptographie symétrique ................... #crypto-sym
        Cryptographie asymétrique .................. #crypto-asym
        Le hachage ................................. #crypto-hash
        Signatures numériques ...................... #crypto-sig
        Protocoles cryptographiques ................ #crypto-proto
        Certificats numériques ..................... #crypto-cert
        Sécurité des mots de passe ................. #crypto-pwd
  04  Protocoles de sécurité ...................... [bientôt]
  05  Sécurité des architectures .................. [bientôt]
  06  Supervision de réseaux ...................... [bientôt]
TD
  TD1  Cryptographie classique .................... #td1
  TD2  Cryptographie moderne ...................... #td2
  TD3  Protocoles cryptographiques ................ #td3
  TD4  Protocoles de sécurité ..................... #td4
TP
  TP1  OpenSSL .................................... #tp1
  TP2  Wireshark & TLS ........................... #tp2
  TP3  Hachage & attaques ........................ #tp3
  TP4  Proxy Squid + SquidGuard .................. #tp4
QUIZ
```

### Menu mobile (largeur < 768 px)

Overlay plein écran avec accordéons `details.acc` imbriqués. Fermeture possible via :
- clic sur un lien de navigation (`onclick="closeMobileMenu()"`)
- clic sur le fond de l'overlay (événement `click` sur `#mobileMenu`)
- touche `Échap` (écouteur sur `document`)

### Comportement du scroll

`scroll-behavior: smooth` est défini sur `<html>`. La classe Tailwind `scroll-mt-24` est appliquée sur les cibles de navigation pour compenser la hauteur de la barre fixe.

Au chargement, `scrollRestoration` est forcé à `'manual'` et `window.scrollTo(0, 0)` est appelé sur les événements `load` et `pageshow`, pour revenir en haut même après un rafraîchissement ou un retour arrière navigateur.

---

## 7. Contenu pédagogique

### Chapitre 01 — Introduction (`#intro`)

Définitions fondamentales :

- **Système informatique** : ensemble des moyens techniques pour faire fonctionner un système d'information
- **Système d'Information (SI)** : ensemble organisé des moyens humains et techniques pour acquérir, stocker, exploiter et diffuser les informations
- **Sécurité des SI (SSI)** : ensemble des mesures structurelles, techniques, organisationnelles et humaines mises en œuvre pour protéger les informations
- **Sécurité informatique** : moyens et techniques pour protéger les actifs informationnels
- **Actifs informationnels** : bases de données, ressources humaines, portail web, code source
- **Chaîne de protection** : trois niveaux imbriqués (sécurité de l'information, du SI, du système informatique)

---

### Chapitre 02 — Généralités sur la Sécurité

#### Cybersécurité (`#cyber`)

Définition : ensemble des outils, politiques, concepts, mécanismes, lignes directrices, méthodes de gestion des risques, actions, bonnes pratiques et technologies utilisés pour protéger les actifs du système informatique.

Pluridisciplinarité : TIC, éthique, normalisation, législation, réglementation.

Acteurs concernés : informaticiens, dirigeants, fournisseurs et partenaires, utilisateurs, tout membre du SI.

Menaces visées : catastrophes naturelles, terrorisme et vol, pirates, hackers, comportements malicieux.

#### Pirates vs Hackers (`#hackers`)

| Profil | Définition |
|---|---|
| Le Pirate | Cherche à piller le système en détruisant ses protections |
| Le Hacker | Exploite des vulnérabilités à des fins personnelles, financières ou politiques |

Trois chapeaux :

| Chapeau | Étiquette | Comportement |
|---|---|---|
| White Hat | Autorisation du propriétaire | Découverte des failles pour améliorer la sécurité |
| Black Hat | Illégal | Exploitation à des fins personnelles ou financières |
| Gray Hat | Ambigu | Détection opportuniste, publication variable des découvertes |

Hackers organisés : cybercriminels, hacktivistes, terroristes, acteurs étatiques.

Sources de menaces : internes (employés, sous-traitants), organisées (cyberactivistes, états), pirates (chapeaux), autres (amateurs, extérieurs).

#### Approche traditionnelle

| Axe | Action | Effet |
|---|---|---|
| Prévention | Empêcher l'incident | Réduire la probabilité (−O) |
| Détection | Identifier l'incident | Surveillance continue |
| Réaction | Répondre et restaurer | Réduire la gravité (−G) |

#### Risques, vulnérabilités, menaces (`#risques`)

Définitions :
- **Risque** : couple (menace, vulnérabilité) qui impacte l'information
- **Menace** : possibilité qu'un événement nuisible (accidentel ou intentionnel) survienne
- **Vulnérabilité** : faiblesse qui expose un système à une attaque
- **Attaque** : exploitation délibérée d'une faiblesse

Natures des vulnérabilités : physiques, technologiques, logicielles, protocoles de communication, acteurs.

Quatre étapes de gestion des risques :
1. Identifier les risques (brainstorming, check-list — types : techniques, humains, fournisseurs)
2. Évaluer le risque — Criticité C = Occurrence (O) × Gravité (G)
3. Apporter une réponse : Éviter (−O), Atténuer (−G), Transférer, Gérer (provision)
4. Suivre les risques : supprimer les passés, surveiller les actifs et latents

Équation synthétique : **Prévention + Protection = Gestion des risques**

#### Matrice interactive des risques (`#matrice`)

Matrice 3×3 (Occurrence × Gravité), survol = info contextuelle dans le panneau droit.

|   | G=1 | G=2 | G=3 |
|---|---|---|---|
| O=1 | R11 — Tolérable | R12 — Tolérable | R13 — Critique |
| O=2 | R21 — Tolérable | R22 — Critique | R23 — Catastrophique |
| O=3 | R31 — Critique | R32 — Catastrophique | R33 — Catastrophique maximal |

Objectif de la gestion : faire passer un risque de R33 vers R11.

#### ISO/IEC 27005 (`#iso`)

Référence internationale de gestion des risques SSI. Adopte le modèle PDCA (Plan-Do-Check-Act) pour l'amélioration continue.

Autres méthodes comparables : NIST SP 800-30, OCTAVE (Carnegie Mellon), IRAM, EBIOS (France), CRAMM (Royaume-Uni), MEHARI (CLUSIF).

#### Triade CID (`#cid`)

| Pilier | Définition | Menaces principales | Contre-mesures |
|---|---|---|---|
| Confidentialité | Accès réservé aux personnes autorisées | Surveillance réseau, vol de fichiers, espionnage, ingénierie sociale | Chiffrement, contrôle d'accès (authentification + autorisation), journalisation |
| Intégrité | Données exactes et non altérées | Modification du trafic, virus, bombes logiques, erreurs humaines | Hachage (MD5, SHA-1, SHA-256, SHA-512), Checksum / CRC |
| Disponibilité | Accès aux ressources en temps voulu | DoS / DDoS, pannes matérielles ou logicielles | Tolérance aux pannes, sauvegardes, mises à jour, surveillance, concept des « cinq neuf » |

Concept des cinq neuf : disponibilité de 99,999 %, soit moins de 5,26 minutes d'interruption par an.

#### Cube de McCumber (`#cube`)

Visualisation 3D animée (rotation CSS de 25 s) avec trois axes orthogonaux :

- **Axe 1 — Trio CID** : Confidentialité, Intégrité, Disponibilité
- **Axe 2 — États des données (S²T)** : Stockage, Traitement, Transmission
- **Axe 3 — Mesures & Personnes** : Politique, Bonne pratique, Personnes

Interaction : le survol met l'animation en pause (`animation-play-state: paused`).

---

### Chapitre 03 — La Cryptographie (`#crypto`)

Contenu présenté sous forme d'accordéons cliquables.

| Section | Contenu principal |
|---|---|
| `#crypto-intro` | Cryptologie, cryptographie, cryptanalyse ; chiffrer / déchiffrer vs crypter / décrypter ; notion de clé ; services de sécurité (confidentialité, authentification, intégrité, disponibilité, non-répudiation, fraîcheur) |
| `#crypto-sym` | César (E(K,X) = (X+K) mod 26), substitution monoalphabétique, Vigenère (polyalphabétique), transposition, principe de Kerckhoffs, XOR, Vernam (1917) ; chiffrement par flux (RC4, A5, E0) vs par bloc (DES, AES, Blowfish) ; modes ECB, CBC (IV), CFB, OFB, CTR ; problème de distribution des clés : N(N−1)/2 pour N personnes |
| `#crypto-asym` | Clé publique / clé privée ; chiffrer avec PubB = confidentialité ; chiffrer avec PrivA = authentification ; RSA (factorisation, 1977) ; Diffie-Hellman (logarithme discret, 1976) avec schéma K = g^ab mod p ; ECDH / ECDSA (courbes elliptiques, 1992) |
| `#crypto-hash` | Propriétés : non-réversible, taille de sortie fixe, résistance aux collisions ; algorithmes : MD5 (128 bits), SHA-1 (160 bits), SHA-2 (256/512 bits), SHA-3 (Keccak) ; application : stockage des mots de passe sous forme d'empreintes |
| `#crypto-sig` | Signature = E(PrivB, H(m)) ; trois services : authentification, non-répudiation, intégrité ; schéma complet émetteur/récepteur ; usages : distribution de logiciels, transactions financières, e-mails |
| `#crypto-proto` | Chiffrement hybride (confidentialité + authentification + intégrité) ; protocole Needham-Schroeder ; HMAC ; attaque MITM : substitution de clé publique, contre-mesures (SAS, certificat, Web of Trust) |
| `#crypto-cert` | SAS (Short Authenticated Strings) ; certificat numérique : structure (nom, clé publique, dates, signature CA), analogie passeport ; SSL/TLS en 5 étapes ; certificat auto-signé vs commercialisé (Symantec, DigiCert) |
| `#crypto-pwd` | Robustesse par longueur : 26^6 ≈ 309 M combinaisons ; robustesse par composition mixte : 36^6 ≈ 2,18 G combinaisons |

---

### Travaux Dirigés (TD) — Pr. Youssou FAYE

| TD | Thème | Contenu |
|---|---|---|
| TD1 | Chiffrement traditionnel | César (K=5), substitution (table fournie), transposition (clé [1-6-4-2-3-5]), Vigenère — message d'étude : `WELCOMETOUASZ` |
| TD2 | Chiffrement moderne | Mode ECB, mode CBC, effet d'avalanche |
| TD3 | Protocoles cryptographiques | Needham-Schroeder, propriété de fraîcheur, authentification mutuelle |
| TD4 | Protocoles de sécurité | Diffie-Hellman (calcul manuel), XOR (M⊕a⊕b), étude de cas : tontine à 4 participants |

---

### Travaux Pratiques (TP) — Dr. Malaw NDIAYE

| TP | Thème | Outils | Contenu |
|---|---|---|---|
| TP1 | Chiffrement avec OpenSSL | `openssl` | Chiffrement symétrique (AES-256-CBC, Base64) ; chiffrement asymétrique RSA (génération de clés, chiffrement hybride) ; empreintes et signatures |
| TP2 | Analyse TLS avec Wireshark | Wireshark, Firefox, OpenSSL | Capture et analyse du handshake TLS ; analyse des certificats ; décryptage via `SSLKEYLOGFILE` ; analyse de sécurité (PFS, cipher suites) ; simulation MITM optionnelle |
| TP3 | Hachage et attaques MD5 | tools4noobs.com, crackstation.net | Attaque par dictionnaire (table fournie) ; attaque par force brute ; limites des bases d'empreintes précalculées |
| TP4 | Proxy Squid + SquidGuard | Squid, SquidGuard, Debian/Ubuntu | Installation et configuration Squid ; ACL (source, destination, horaires) ; SquidGuard avec blacklists Toulouse ; authentification basique (htpasswd) ; limitation de bande passante (delay pools) ; analyse des logs avec awk |

---

## 8. Système de quiz interactif

### Structure des données (`quizData`)

Tableau JavaScript de 29 objets avec la structure suivante :

```javascript
{
  q       : "Texte de la question",
  options : ["Option A", "Option B", "Option C", "Option D"],
  correct : 1   // index 0-based de la bonne réponse
}
```

### Répartition des questions par thème

| Thème | Nombre |
|---|---|
| Fondamentaux SI et SSI | 2 |
| Trio CID | 2 |
| Pirates et hackers | 2 |
| Risques (définitions, calcul, ISO/IEC 27005) | 3 |
| Triade CID — contre-mesures | 2 |
| Cryptographie classique (César, Vigenère, Kerckhoffs) | 4 |
| Cryptographie symétrique moderne (ECB, CBC) | 3 |
| Cryptographie asymétrique (RSA, Diffie-Hellman) | 4 |
| Hachage et signatures numériques | 3 |
| Protocoles (Needham-Schroeder, MITM, certificats, hybride) | 3 |
| Attaque XOR | 1 |
| **Total** | **29** |

### Flux d'exécution

```
loadQuestion()
    Affichage de la question et des 4 options
        |
selectOption(idx, el)
    Correct  → classe "correct" sur l'option ; score++
    Incorrect → classe "wrong" sur l'option ; classe "correct" sur la bonne réponse
        |
    Timeout 1 500 ms → question suivante
        |
    [Dernière question] → showResult()
        score = 100 %   → "Parfait ! Vous maîtrisez..."
        score >= 80 %   → "Excellent travail !"
        score >= 60 %   → "Bon travail !"
        score >= 40 %   → "Passable. Il est recommandé..."
        score <  40 %   → "À retravailler. Reprenez..."
        |
restartQuiz()
    currentQ = 0, score = 0 → loadQuestion()
```

### Variables d'état

```javascript
let currentQ = 0;     // index de la question courante (0-based)
let score    = 0;     // nombre de bonnes réponses
let answered = false; // verrou anti-double-clic
```

---

## 9. JavaScript — fonctionnalités

### Particules d'arrière-plan

Au chargement, 30 éléments `.particle` sont injectés dans `#particles` avec position horizontale et durée d'animation aléatoires :

```javascript
for(let i = 0; i < 30; i++) {
  p.style.left              = Math.random() * 100 + '%';
  p.style.animationDelay    = Math.random() * 8 + 's';
  p.style.animationDuration = (6 + Math.random() * 6) + 's';
}
```

### Fonctions utilitaires

| Fonction | Rôle |
|---|---|
| `toggleMobileMenu()` | Ouvre ou ferme le menu mobile, verrouille le scroll du `body` |
| `closeMobileMenu()` | Ferme le menu et restaure les icônes et le scroll |
| `showToast(msg)` | Affiche un message flottant pendant 2 500 ms |
| `toggleCard(el)` | Micro-animation de pulsation sur une carte au clic |
| `selectTree(el)` | Sélectionne un scénario de l'arbre de risques (contour rouge) |

### Interactions spécifiques

| Élément | Comportement |
|---|---|
| `.matrix-cell:mouseenter` | Mise à jour dynamique de la carte `#matrixInfo` avec les détails du risque |
| `#cubeScene:mouseenter / mouseleave` | Pause / reprise de l'animation CSS du cube McCumber |
| `.cid-card:click` | Affiche un toast avec la description du pilier CID correspondant |
| `#mobileMenu:click` | Ferme le menu si le clic cible directement le fond (pas un lien) |
| `document:keydown(Escape)` | Ferme le menu mobile |

---

## 10. Responsive design

| Breakpoint Tailwind | Largeur | Comportement |
|---|---|---|
| — (mobile) | < 640 px | Toast pleine largeur en bas, slide-up ; cube réduit à 80 % |
| `sm:` | >= 640 px | Bouton "START QUIZ" visible dans la nav |
| `md:` | >= 768 px | Grilles 2 colonnes pour les cartes ; menu desktop visible |
| `lg:` | >= 1024 px | Grilles 3 colonnes ; hero en 12 colonnes (7+5) |

---

## 11. SEO et accessibilité

### SEO présent

```html
<title>Sécurité des Réseaux — Cours Interactif | Pr. Youssou FAYE</title>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<html lang="fr">
```

### Point manquant

La balise `<meta name="description">` est absente. Il est recommandé de l'ajouter :

```html
<meta name="description" content="Cours interactif de Sécurité des Réseaux — L3 Ingénierie Informatique, UASZ. Chapitres, TD, TP et quiz sur la cryptographie et la cybersécurité.">
```

### Structure sémantique

- `<nav>` pour la navigation principale
- `<header>` pour la section hero
- `<section>` pour chaque bloc thématique identifié par un `id`
- `<footer>` pour les informations institutionnelles
- `<details>` / `<summary>` natifs pour les accordéons (navigables au clavier)

### Points d'amélioration accessibilité

- Les `<button>` de navigation n'ont pas d'attribut `aria-label` ou `aria-expanded`
- Les dropdowns déclenchés au survol CSS (`:hover`) ne sont pas accessibles au clavier
- Les éléments cliquables `div.cid-card` et `div.card[onclick]` devraient avoir `role="button"` et `tabindex="0"`

---

## 12. Guide de contribution

### Ajouter un nouveau chapitre (exemple : Chapitre 04)

**Étape 1 — Section de contenu**

Dupliquer un bloc `<section>` existant et modifier son identifiant :

```html
<section id="chap4" class="py-24 relative border-t border-cyan-500/10">
  <div class="max-w-7xl mx-auto px-6">
    <!-- contenu du chapitre -->
  </div>
</section>
```

**Étape 2 — Menu desktop**

Dans `.dropdown-panel` du bouton "PLAN DU COURS", remplacer la ligne disabled :

```html
<div class="dropdown-row">
  <a href="#chap4" class="dropdown-link">
    <span class="num">04</span>Protocoles de sécurité
  </a>
</div>
```

**Étape 3 — Menu mobile**

Dans `#mobileMenu`, dans le `details.acc` du plan du cours :

```html
<a href="#chap4" class="mob-link" onclick="closeMobileMenu()">
  04 · Protocoles de sécurité
</a>
```

**Étape 4 — Grille du plan du cours**

Remplacer la carte "bientôt" correspondante par un lien actif :

```html
<a href="#chap4" class="card p-6 block">
  <div class="flex items-start justify-between mb-3">
    <span class="font-mono text-xs text-cyan-400">CHAPITRE 04</span>
    <i class="fa-solid fa-handshake text-cyan-400"></i>
  </div>
  <h3 class="text-xl font-bold mb-2">Protocoles de sécurité</h3>
  <p class="text-gray-400 text-sm">Description courte.</p>
</a>
```

---

### Ajouter un TD ou un TP

**Pour un TD5 :**

1. Dupliquer le bloc `<div id="td4" ...>` et créer `<div id="td5" ...>`
2. Ajouter une carte dans la grille `TD_INDEX` :

```html
<a href="#td5" class="index-card" style="border-color:rgba(255,184,0,0.18)">
  <div class="font-mono text-xs mb-2" style="color:var(--warning)">TD 5</div>
  <div class="font-bold mb-1">Titre du TD</div>
  <div class="text-xs text-gray-500">Sous-titre descriptif</div>
</a>
```

3. Ajouter le lien dans le dropdown `TD` du menu desktop et dans le `details.acc` du menu mobile.

**Pour un TP5 :** même procédure sur la section `#tp`, grille `TP_INDEX` et menus.

---

### Ajouter des questions au quiz

Dans le tableau `quizData` (ligne 3188 environ de `index.html`), insérer un objet de plus :

```javascript
{
  q: "Votre question ?",
  options: [
    "Option A",
    "Option B",
    "Option C",   // bonne réponse si correct: 2
    "Option D"
  ],
  correct: 2
}
```

Le compteur total de questions se met à jour automatiquement dans l'interface.

---

## 13. Roadmap — Chapitres futurs

| Chapitre | Titre | État |
|---|---|---|
| 01 | Introduction | Complet |
| 02 | Généralités sur la sécurité | Complet |
| 03 | La Cryptographie | Complet |
| 04 | Protocoles de sécurité | A venir |
| 05 | Sécurité des architectures | A venir |
| 06 | Supervision de réseaux | A venir |

---

## 14. Annexes

### Annexe A — Identifiants des sections

| Ancre | Contenu |
|---|---|
| `#intro` | Définitions fondamentales (Chapitre 01) |
| `#cyber` | Cybersécurité |
| `#hackers` | Pirates vs Hackers |
| `#risques` | Risques / Vulnérabilités / Menaces |
| `#matrice` | Matrice interactive des risques |
| `#iso` | ISO/IEC 27005 et PDCA |
| `#cid` | Triade CID |
| `#cube` | Cube de McCumber |
| `#crypto` | Section cryptographie (Chapitre 03) |
| `#crypto-intro` | Introduction et définitions |
| `#crypto-sym` | Cryptographie symétrique |
| `#crypto-asym` | Cryptographie asymétrique |
| `#crypto-hash` | Fonctions de hachage |
| `#crypto-sig` | Signatures numériques |
| `#crypto-proto` | Protocoles cryptographiques |
| `#crypto-cert` | Certificats numériques |
| `#crypto-pwd` | Sécurité des mots de passe |
| `#td` | Section TD (index) |
| `#td1` | TD1 — Chiffrement traditionnel |
| `#td2` | TD2 — Chiffrement moderne |
| `#td3` | TD3 — Protocoles cryptographiques |
| `#td4` | TD4 — Protocoles de sécurité |
| `#tp` | Section TP (index) |
| `#tp1` | TP1 — OpenSSL |
| `#tp2` | TP2 — Wireshark et TLS |
| `#tp3` | TP3 — Hachage et attaques |
| `#tp4` | TP4 — Proxy Squid + SquidGuard |
| `#quiz` | Quiz interactif |

### Annexe B — Métriques du projet

| Métrique | Valeur |
|---|---|
| Taille du fichier | ~199 Ko |
| Nombre de lignes total | 3 580 |
| Lignes CSS custom (inline) | ~470 |
| Lignes JavaScript (inline) | ~490 |
| Lignes HTML | ~2 620 |
| Questions de quiz | 29 |
| Chapitres de cours complets | 3 |
| TD | 4 |
| TP | 4 |
| Accordéons `details.acc` | 26+ |
| Dépendances externes | 3 (Tailwind, Google Fonts, Font Awesome) |

---

*Documentation rédigée le 28 septembre 2026 — SEC.NET v2025-2026*
