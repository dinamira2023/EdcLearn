# Document d'Analyse

## Plateforme Éducative Intelligente avec Recommandations d'Apprentissage Personnalisées

---

**Auteurs** : Dina & Leticia  
**Date** : Avril 2026  
**Version** : 1.0

---

## Table des matières

1. [Introduction](#1-introduction)
2. [Analyse des besoins](#2-analyse-des-besoins)
3. [Acteurs du système](#3-acteurs-du-système)
4. [Diagramme de cas d'utilisation](#4-diagramme-de-cas-dutilisation)
5. [Diagramme de classes](#5-diagramme-de-classes)
6. [Diagramme d'activités](#6-diagramme-dactivités)
7. [Diagramme de séquence](#7-diagramme-de-séquence)
8. [Modélisation de la base de données (diagramme ER)](#8-modélisation-de-la-base-de-données)
9. [Architecture technique](#9-architecture-technique)
10. [Défis et solutions](#10-défis-et-solutions)
11. [Calendrier prévisionnel](#11-calendrier-prévisionnel)

---

## 1. Introduction

### 1.1 Contexte du projet

De nombreux étudiants éprouvent des difficultés à identifier les ressources d'apprentissage qui correspondent à leur niveau de compétences ou à leurs besoins spécifiques. Les plateformes éducatives actuelles manquent souvent de personnalisation, ce qui ralentit la progression des apprenants et crée un fossé entre les contenus disponibles et les besoins réels.

### 1.2 Objectif

Développer une application web et mobile qui propose des **parcours d'apprentissage personnalisés** pour les étudiants en fonction de leur niveau, de leurs compétences et de leur progression. En utilisant l'intelligence artificielle, l'application recommande des ressources pédagogiques adaptées (vidéos, articles, exercices) et des cours supplémentaires pour combler les lacunes ou approfondir certaines compétences.

### 1.3 Portée

Le système couvre les fonctionnalités suivantes :
- Gestion des utilisateurs (étudiants, enseignants, administrateurs)
- Gestion des cours, modules et ressources pédagogiques
- Moteur de recommandations alimenté par l'IA
- Suivi de la progression des étudiants en temps réel
- Évaluation via des quiz et des exercices
- Interactions sociales (forums, commentaires)

---

## 2. Analyse des besoins

### 2.1 Besoins fonctionnels

| ID    | Besoin                                      | Priorité |
|-------|---------------------------------------------|----------|
| BF-01 | Inscription et authentification sécurisée (JWT) | Haute    |
| BF-02 | Gestion des profils utilisateurs avec rôles (Étudiant, Enseignant, Admin) | Haute    |
| BF-03 | Création et gestion de cours par les enseignants | Haute    |
| BF-04 | Organisation des cours en modules et ressources | Haute    |
| BF-05 | Recommandations personnalisées de ressources via IA | Haute    |
| BF-06 | Passage de quiz et évaluation des compétences | Haute    |
| BF-07 | Tableau de bord de suivi de la progression | Haute    |
| BF-08 | Définition d'objectifs d'apprentissage personnels | Moyenne  |
| BF-09 | Forum de discussion et commentaires sur les cours | Moyenne  |
| BF-10 | Notifications de nouvelles ressources recommandées | Moyenne  |
| BF-11 | Recherche et filtrage des cours et ressources | Moyenne  |
| BF-12 | Tableau de bord administrateur (statistiques globales) | Basse    |

### 2.2 Besoins non fonctionnels

| ID     | Besoin                                        | Critère                                    |
|--------|-----------------------------------------------|--------------------------------------------|
| BNF-01 | Performance                                   | Temps de réponse API < 500 ms              |
| BNF-02 | Scalabilité                                   | Support de 10 000+ utilisateurs simultanés |
| BNF-03 | Sécurité                                      | Chiffrement bcrypt, JWT, HTTPS, RGPD       |
| BNF-04 | Disponibilité                                 | Uptime ≥ 99,5 %                            |
| BNF-05 | Compatibilité                                 | Web (Chrome, Firefox, Safari) + Mobile     |
| BNF-06 | Maintenabilité                                | Architecture microservices, code modulaire |
| BNF-07 | Protection des données                        | Conformité RGPD / CCPA                     |

---

## 3. Acteurs du système

| Acteur        | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| **Étudiant**  | Utilisateur principal. Consulte les cours, passe des quiz, reçoit des recommandations personnalisées et suit sa progression. |
| **Enseignant**| Crée et gère les cours, modules et ressources. Consulte les résultats de ses étudiants. |
| **Administrateur** | Gère les utilisateurs, supervise la plateforme, accède aux statistiques globales et modère le contenu. |
| **Système IA**| Acteur interne. Analyse les données de progression et génère les recommandations personnalisées. |

---

## 4. Diagramme de cas d'utilisation

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                     PLATEFORME ÉDUCATIVE INTELLIGENTE                           │
│                                                                                 │
│  ┌──────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                          │   │
│  │   (S'inscrire)──────────────────┐                                        │   │
│  │                                 │                                        │   │
│  │   (Se connecter)────────────────┤                                        │   │
│  │                                 │                                        │   │
│  │   (Gérer son profil)────────────┤                                        │   │
│  │                                 │         ┌──────────┐                   │   │
│  │   (Consulter les cours)─────────┼─────────│ Étudiant │                   │   │
│  │                                 │         └──────────┘                   │   │
│  │   (Passer un quiz)─────────────┤                                        │   │
│  │                                 │                                        │   │
│  │   (Voir sa progression)─────────┤                                        │   │
│  │                                 │                                        │   │
│  │   (Recevoir des recommandations)┤                                        │   │
│  │                                 │                                        │   │
│  │   (Participer au forum)─────────┤                                        │   │
│  │                                 │                                        │   │
│  │   (Définir des objectifs)───────┘                                        │   │
│  │                                                                          │   │
│  │   ─────────────────────────────────────────────────────────              │   │
│  │                                                                          │   │
│  │   (Créer un cours)──────────────┐                                        │   │
│  │                                 │         ┌────────────┐                 │   │
│  │   (Gérer les modules)───────────┼─────────│ Enseignant │                 │   │
│  │                                 │         └────────────┘                 │   │
│  │   (Ajouter des ressources)──────┤                                        │   │
│  │                                 │                                        │   │
│  │   (Voir résultats étudiants)────┘                                        │   │
│  │                                                                          │   │
│  │   ─────────────────────────────────────────────────────────              │   │
│  │                                                                          │   │
│  │   (Gérer les utilisateurs)──────┐         ┌───────────────┐             │   │
│  │                                 ├─────────│ Administrateur│             │   │
│  │   (Modérer le contenu)──────────┤         └───────────────┘             │   │
│  │                                 │                                        │   │
│  │   (Consulter statistiques)──────┘                                        │   │
│  │                                                                          │   │
│  │   ─────────────────────────────────────────────────────────              │   │
│  │                                                                          │   │
│  │   (Analyser la progression)─────┐         ┌────────────┐                │   │
│  │                                 ├─────────│ Système IA │                │   │
│  │   (Générer recommandations)─────┘         └────────────┘                │   │
│  │                                                                          │   │
│  └──────────────────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────────────────┘
```

### 4.1 Description des cas d'utilisation principaux

#### CU-01 : S'inscrire
- **Acteur** : Étudiant, Enseignant
- **Précondition** : L'utilisateur n'a pas de compte existant
- **Scénario principal** :
  1. L'utilisateur accède au formulaire d'inscription
  2. Il renseigne son nom, email, mot de passe et rôle
  3. Le système valide les données (email unique, rôle valide)
  4. Le système hash le mot de passe (bcrypt) et crée le compte
  5. Le système génère un token JWT et le retourne
- **Scénario alternatif** : Email déjà utilisé → erreur 409

#### CU-02 : Se connecter
- **Acteur** : Étudiant, Enseignant, Administrateur
- **Précondition** : L'utilisateur possède un compte
- **Scénario principal** :
  1. L'utilisateur saisit email et mot de passe
  2. Le système vérifie les identifiants
  3. Le système génère et retourne un token JWT
- **Scénario alternatif** : Identifiants incorrects → erreur 401

#### CU-03 : Recevoir des recommandations personnalisées
- **Acteur** : Étudiant, Système IA
- **Précondition** : L'étudiant est connecté et a une historique de progression
- **Scénario principal** :
  1. L'étudiant consulte son tableau de bord
  2. Le système IA analyse ses résultats de quiz, ses cours suivis et ses objectifs
  3. Le moteur de recommandation applique le filtrage collaboratif et le filtrage basé sur le contenu
  4. Le système affiche les ressources recommandées classées par pertinence
- **Scénario alternatif** : Nouvel étudiant sans historique → recommandations basées sur le profil initial (cold start)

#### CU-04 : Créer un cours
- **Acteur** : Enseignant
- **Précondition** : L'enseignant est connecté avec le rôle "Enseignant"
- **Scénario principal** :
  1. L'enseignant accède au formulaire de création de cours
  2. Il renseigne le titre et la description
  3. Il ajoute des modules au cours
  4. Il ajoute des ressources (vidéos, articles, exercices) à chaque module
  5. Le système enregistre le cours et le rend disponible

#### CU-05 : Passer un quiz
- **Acteur** : Étudiant
- **Précondition** : L'étudiant est inscrit au cours contenant le quiz
- **Scénario principal** :
  1. L'étudiant sélectionne un quiz associé à un cours
  2. Le système affiche les questions
  3. L'étudiant répond aux questions et soumet le quiz
  4. Le système calcule le score et met à jour la progression
  5. Le système IA ajuste les recommandations en conséquence

---

## 5. Diagramme de classes

```
┌─────────────────────────┐       ┌─────────────────────────┐
│      Utilisateur        │       │          Cours          │
├─────────────────────────┤       ├─────────────────────────┤
│ - id: int (PK)          │       │ - idCours: int (PK)     │
│ - nom: str              │       │ - titre: str            │
│ - email: str (UNIQUE)   │       │ - description: str      │
│ - mot_de_passe_hash: str│       │ - idEnseignant: int (FK)│
│ - role: str             │       │ - date_creation: date   │
│ - created_at: datetime  │       │ - categorie: str        │
├─────────────────────────┤       ├─────────────────────────┤
│ + s_inscrire()          │       │ + creer()               │
│ + se_connecter()        │ 1   * │ + modifier()            │
│ + modifier_profil()     │───────│ + supprimer()           │
│ + definir_objectif()    │crée   │ + ajouter_module()      │
└────────┬────────────────┘       └──────────┬──────────────┘
         │                                    │
         │                                    │ 1
         │                                    │
         │                                    │ *
         │                        ┌───────────┴─────────────┐
         │                        │         Module          │
         │                        ├─────────────────────────┤
         │                        │ - idModule: int (PK)    │
         │                        │ - titre: str            │
         │                        │ - ordre: int            │
         │                        │ - idCours: int (FK)     │
         │                        ├─────────────────────────┤
         │                        │ + creer()               │
         │                        │ + modifier()            │
         │                        └──────────┬──────────────┘
         │                                    │ 1
         │                                    │
         │                                    │ *
         │                        ┌───────────┴─────────────┐
         │                        │       Ressource         │
         │                        ├─────────────────────────┤
         │                        │ - idRessource: int (PK) │
         │                        │ - type: str             │
         │                        │ - contenu: str          │
         │                        │ - url: str              │
         │                        │ - idModule: int (FK)    │
         │                        ├─────────────────────────┤
         │                        │ + ajouter()             │
         │                        │ + consulter()           │
         │                        └─────────────────────────┘
         │
         │ 1
         │
         │ *
┌────────┴────────────────┐       ┌─────────────────────────┐
│         Quiz            │       │     Recommandation      │
├─────────────────────────┤       ├─────────────────────────┤
│ - idQuiz: int (PK)      │       │ - idRecommandation: int │
│ - score: float          │       │ - idEtudiant: int (FK)  │
│ - date_passage: date    │       │ - idRessource: int (FK) │
│ - idCours: int (FK)     │       │ - score_pertinence: float│
│ - idEtudiant: int (FK)  │       │ - date_generation: date │
├─────────────────────────┤       │ - statut: str           │
│ + passer()              │       ├─────────────────────────┤
│ + calculer_score()      │       │ + generer()             │
│ + afficher_resultat()   │       │ + consulter()           │
└─────────────────────────┘       │ + marquer_vue()         │
                                  └─────────────────────────┘
         │
┌────────┴────────────────┐       ┌─────────────────────────┐
│      Progression        │       │    ObjectifApprentissage │
├─────────────────────────┤       ├─────────────────────────┤
│ - idProgression: int    │       │ - idObjectif: int (PK)  │
│ - idEtudiant: int (FK)  │       │ - idEtudiant: int (FK)  │
│ - idCours: int (FK)     │       │ - description: str      │
│ - pourcentage: float    │       │ - date_cible: date      │
│ - derniere_activite: dt │       │ - statut: str           │
├─────────────────────────┤       ├─────────────────────────┤
│ + mettre_a_jour()       │       │ + definir()             │
│ + consulter()           │       │ + modifier()            │
└─────────────────────────┘       │ + verifier_atteinte()   │
                                  └─────────────────────────┘

┌─────────────────────────┐       ┌─────────────────────────┐
│      ForumPost          │       │      Commentaire        │
├─────────────────────────┤       ├─────────────────────────┤
│ - idPost: int (PK)      │       │ - idCommentaire: int    │
│ - titre: str            │       │ - contenu: str          │
│ - contenu: str          │       │ - date_creation: date   │
│ - date_creation: date   │       │ - idAuteur: int (FK)    │
│ - idAuteur: int (FK)    │       │ - idPost: int (FK)      │
│ - idCours: int (FK)     │       ├─────────────────────────┤
├─────────────────────────┤       │ + ajouter()             │
│ + publier()             │ 1   * │ + modifier()            │
│ + modifier()            │───────│ + supprimer()           │
│ + supprimer()           │       └─────────────────────────┘
└─────────────────────────┘

Relations :
  Utilisateur (1) ──── (*) Cours          : Un enseignant crée plusieurs cours
  Utilisateur (1) ──── (*) Quiz           : Un étudiant passe plusieurs quiz
  Utilisateur (1) ──── (*) Progression    : Un étudiant a une progression par cours
  Utilisateur (1) ──── (*) Recommandation : Un étudiant reçoit plusieurs recommandations
  Utilisateur (1) ──── (*) ObjectifApprentissage : Un étudiant définit plusieurs objectifs
  Cours        (1) ──── (*) Module        : Un cours contient plusieurs modules
  Module       (1) ──── (*) Ressource     : Un module contient plusieurs ressources
  Cours        (1) ──── (*) Quiz          : Un cours a plusieurs quiz
  Ressource    (1) ──── (*) Recommandation: Une ressource peut être recommandée à plusieurs étudiants
  Cours        (1) ──── (*) ForumPost     : Un cours a un forum de discussion
  ForumPost    (1) ──── (*) Commentaire   : Un post reçoit plusieurs commentaires
```

---

## 6. Diagramme d'activités

### 6.1 Activité : Processus de recommandation personnalisée

```
            ┌───────────┐
            │  Début    │
            └─────┬─────┘
                  │
                  ▼
        ┌─────────────────┐
        │ Étudiant se     │
        │ connecte        │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ Charger profil  │
        │ et historique   │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ Collecter les   │
        │ données :       │
        │ - Quiz passés   │
        │ - Cours suivis  │
        │ - Objectifs     │
        │ - Préférences   │
        └────────┬────────┘
                 │
                 ▼
     ┌───────────────────────┐
     │  L'étudiant a-t-il    │
     │  un historique ?      │
     └───┬───────────────┬───┘
         │ Oui           │ Non
         ▼               ▼
┌────────────────┐ ┌──────────────────┐
│ Filtrage       │ │ Recommandations  │
│ collaboratif + │ │ basées sur le    │
│ filtrage basé  │ │ profil initial   │
│ sur le contenu │ │ (cold start)     │
└───────┬────────┘ └────────┬─────────┘
        │                   │
        └────────┬──────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ Calculer scores │
        │ de pertinence   │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ Trier et filtrer│
        │ les ressources  │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ Afficher les    │
        │ recommandations │
        │ au tableau de   │
        │ bord            │
        └────────┬────────┘
                 │
                 ▼
     ┌───────────────────────┐
     │ L'étudiant consulte   │
     │ une ressource ?       │
     └───┬───────────────┬───┘
         │ Oui           │ Non
         ▼               │
┌────────────────┐       │
│ Mettre à jour  │       │
│ la progression │       │
│ et le feedback │       │
└───────┬────────┘       │
        │                │
        ▼                │
┌────────────────┐       │
│ Ajuster les    │       │
│ recommandations│       │
│ futures        │       │
└───────┬────────┘       │
        │                │
        └────────┬───────┘
                 │
                 ▼
            ┌────────┐
            │  Fin   │
            └────────┘
```

### 6.2 Activité : Inscription et création de compte

```
            ┌───────────┐
            │  Début    │
            └─────┬─────┘
                  │
                  ▼
        ┌─────────────────┐
        │ Accéder au      │
        │ formulaire      │
        │ d'inscription   │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ Saisir :        │
        │ - Nom           │
        │ - Email         │
        │ - Mot de passe  │
        │ - Rôle          │
        └────────┬────────┘
                 │
                 ▼
     ┌───────────────────────┐
     │  Le rôle est-il       │
     │  valide ?             │
     └───┬───────────────┬───┘
         │ Oui           │ Non
         ▼               ▼
         │       ┌───────────────┐
         │       │ Erreur 400 :  │
         │       │ Rôle invalide │
         │       └───────┬───────┘
         │               │
         │               ▼
         │          ┌────────┐
         │          │  Fin   │
         │          └────────┘
         ▼
     ┌───────────────────────┐
     │  L'email est-il       │
     │  déjà utilisé ?       │
     └───┬───────────────┬───┘
         │ Non           │ Oui
         ▼               ▼
         │       ┌───────────────┐
         │       │ Erreur 409 :  │
         │       │ Email existant│
         │       └───────┬───────┘
         │               │
         │               ▼
         │          ┌────────┐
         │          │  Fin   │
         │          └────────┘
         ▼
┌─────────────────┐
│ Hasher le mot   │
│ de passe        │
│ (bcrypt)        │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Créer l'objet   │
│ Utilisateur     │
│ en base         │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Générer token   │
│ JWT             │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Retourner le    │
│ token au client │
└────────┬────────┘
         │
         ▼
    ┌────────┐
    │  Fin   │
    └────────┘
```

---

## 7. Diagramme de séquence

### 7.1 Séquence : Inscription (Signup)

```
┌──────────┐          ┌──────────┐          ┌──────────┐          ┌──────────┐
│  Client  │          │ API Auth │          │    DB    │          │   JWT    │
│ (Frontend)│         │ (FastAPI)│          │(PostgreSQL)│        │  Module  │
└────┬─────┘          └────┬─────┘          └────┬─────┘          └────┬─────┘
     │                     │                     │                     │
     │ POST /auth/signup   │                     │                     │
     │ {nom, email,        │                     │                     │
     │  mot_de_passe, role}│                     │                     │
     │────────────────────>│                     │                     │
     │                     │                     │                     │
     │                     │ Valider le rôle     │                     │
     │                     │ (Etudiant/Enseignant│                     │
     │                     │  /Admin)            │                     │
     │                     │─────┐               │                     │
     │                     │     │               │                     │
     │                     │<────┘               │                     │
     │                     │                     │                     │
     │                     │ SELECT email        │                     │
     │                     │────────────────────>│                     │
     │                     │                     │                     │
     │                     │ Résultat: null      │                     │
     │                     │<────────────────────│                     │
     │                     │                     │                     │
     │                     │ hash_password()     │                     │
     │                     │─────┐               │                     │
     │                     │     │ bcrypt         │                     │
     │                     │<────┘               │                     │
     │                     │                     │                     │
     │                     │ INSERT utilisateur  │                     │
     │                     │────────────────────>│                     │
     │                     │                     │                     │
     │                     │ OK (user créé)      │                     │
     │                     │<────────────────────│                     │
     │                     │                     │                     │
     │                     │ create_access_token(│                     │
     │                     │   id, role)         │                     │
     │                     │────────────────────────────────────────>  │
     │                     │                     │                     │
     │                     │        JWT token    │                     │
     │                     │<────────────────────────────────────────  │
     │                     │                     │                     │
     │ 200 {access_token}  │                     │                     │
     │<────────────────────│                     │                     │
     │                     │                     │                     │
```

### 7.2 Séquence : Connexion (Login)

```
┌──────────┐          ┌──────────┐          ┌──────────┐          ┌──────────┐
│  Client  │          │ API Auth │          │    DB    │          │   JWT    │
│ (Frontend)│         │ (FastAPI)│          │(PostgreSQL)│        │  Module  │
└────┬─────┘          └────┬─────┘          └────┬─────┘          └────┬─────┘
     │                     │                     │                     │
     │ POST /auth/login    │                     │                     │
     │ {email,             │                     │                     │
     │  mot_de_passe}      │                     │                     │
     │────────────────────>│                     │                     │
     │                     │                     │                     │
     │                     │ SELECT par email    │                     │
     │                     │────────────────────>│                     │
     │                     │                     │                     │
     │                     │ Utilisateur trouvé  │                     │
     │                     │<────────────────────│                     │
     │                     │                     │                     │
     │                     │ verify_password()   │                     │
     │                     │─────┐               │                     │
     │                     │     │ bcrypt verify  │                     │
     │                     │<────┘               │                     │
     │                     │                     │                     │
     │                     │ create_access_token │                     │
     │                     │────────────────────────────────────────>  │
     │                     │                     │                     │
     │                     │        JWT token    │                     │
     │                     │<────────────────────────────────────────  │
     │                     │                     │                     │
     │ 200 {access_token}  │                     │                     │
     │<────────────────────│                     │                     │
     │                     │                     │                     │
```

### 7.3 Séquence : Obtenir des recommandations personnalisées

```
┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
│  Client  │     │ API      │     │ Moteur   │     │ DB SQL   │     │ DB NoSQL │
│(Frontend)│     │ Gateway  │     │ Reco IA  │     │(Postgres)│     │(MongoDB) │
└────┬─────┘     └────┬─────┘     └────┬─────┘     └────┬─────┘     └────┬─────┘
     │                │                │                │                │
     │ GET /reco      │                │                │                │
     │ [JWT token]    │                │                │                │
     │───────────────>│                │                │                │
     │                │                │                │                │
     │                │ Valider JWT    │                │                │
     │                │───┐            │                │                │
     │                │   │            │                │                │
     │                │<──┘            │                │                │
     │                │                │                │                │
     │                │ GET /reco/{id} │                │                │
     │                │───────────────>│                │                │
     │                │                │                │                │
     │                │                │ Charger profil │                │
     │                │                │ + historique   │                │
     │                │                │───────────────>│                │
     │                │                │                │                │
     │                │                │ Données        │                │
     │                │                │ progression    │                │
     │                │                │<───────────────│                │
     │                │                │                │                │
     │                │                │ Charger        │                │
     │                │                │ ressources     │                │
     │                │                │ disponibles    │                │
     │                │                │───────────────────────────────>│
     │                │                │                │                │
     │                │                │ Catalogue      │                │
     │                │                │ ressources     │                │
     │                │                │<───────────────────────────────│
     │                │                │                │                │
     │                │                │ Appliquer      │                │
     │                │                │ filtrage       │                │
     │                │                │ collaboratif + │                │
     │                │                │ content-based  │                │
     │                │                │───┐            │                │
     │                │                │   │ scoring    │                │
     │                │                │<──┘            │                │
     │                │                │                │                │
     │                │ Recommandations│                │                │
     │                │ triées         │                │                │
     │                │<───────────────│                │                │
     │                │                │                │                │
     │ 200 [{reco1},  │                │                │                │
     │  {reco2}, ...] │                │                │                │
     │<───────────────│                │                │                │
     │                │                │                │                │
```

---

## 8. Modélisation de la base de données

### 8.1 Modèle Logique de Données (MLD)

```
UTILISATEUR (id PK, nom, email UNIQUE, mot_de_passe_hash, role, created_at)
COURS (idCours PK, titre, description, categorie, date_creation, idEnseignant FK → UTILISATEUR.id)
MODULE (idModule PK, titre, ordre, idCours FK → COURS.idCours)
RESSOURCE (idRessource PK, type, contenu, url, idModule FK → MODULE.idModule)
QUIZ (idQuiz PK, score, date_passage, idCours FK → COURS.idCours, idEtudiant FK → UTILISATEUR.id)
PROGRESSION (idProgression PK, pourcentage, derniere_activite, idEtudiant FK → UTILISATEUR.id, idCours FK → COURS.idCours)
RECOMMANDATION (idRecommandation PK, score_pertinence, date_generation, statut, idEtudiant FK → UTILISATEUR.id, idRessource FK → RESSOURCE.idRessource)
OBJECTIF_APPRENTISSAGE (idObjectif PK, description, date_cible, statut, idEtudiant FK → UTILISATEUR.id)
FORUM_POST (idPost PK, titre, contenu, date_creation, idAuteur FK → UTILISATEUR.id, idCours FK → COURS.idCours)
COMMENTAIRE (idCommentaire PK, contenu, date_creation, idAuteur FK → UTILISATEUR.id, idPost FK → FORUM_POST.idPost)
```

### 8.2 Diagramme Entité-Relation (ER)

```
┌──────────────────┐         ┌──────────────────┐         ┌──────────────────┐
│   UTILISATEUR    │         │      COURS       │         │     MODULE       │
├──────────────────┤         ├──────────────────┤         ├──────────────────┤
│ *id          INT │───┐     │ *idCours     INT │───┐     │ *idModule    INT │
│  nom     VARCHAR │   │     │  titre   VARCHAR │   │     │  titre   VARCHAR │
│  email   VARCHAR │   │     │  description TEXT│   │     │  ordre       INT │
│  mot_de_passe    │   │     │  categorie   VAR │   │     │  idCours     INT │──FK
│    _hash VARCHAR │   │     │  date_creation DT│   │     └──────────────────┘
│  role    VARCHAR │   │     │  idEnseignant INT│──FK          │
│  created_at   DT │   │     └──────────────────┘             │ 1:N
└──────────────────┘   │          │                            │
     │  │  │  │        │          │ 1:N                  ┌──────────────────┐
     │  │  │  │        │          │                      │   RESSOURCE      │
     │  │  │  │        │    ┌──────────────────┐         ├──────────────────┤
     │  │  │  │        │    │      QUIZ        │         │ *idRessource INT │
     │  │  │  │        │    ├──────────────────┤         │  type    VARCHAR │
     │  │  │  │    1:N │    │ *idQuiz      INT │         │  contenu    TEXT │
     │  │  │  └────────┼───>│  score     FLOAT │         │  url     VARCHAR │
     │  │  │           │    │  date_passage DT │         │  idModule    INT │──FK
     │  │  │           │    │  idCours     INT │──FK     └──────────────────┘
     │  │  │           │    │  idEtudiant  INT │──FK          │
     │  │  │           │    └──────────────────┘              │
     │  │  │           │                                      │ 1:N
     │  │  │  1:N      │                                      │
     │  │  └───────────┼──────────────────────────────┐  ┌──────────────────┐
     │  │              │                              │  │ RECOMMANDATION   │
     │  │              │    ┌──────────────────┐      │  ├──────────────────┤
     │  │              │    │   PROGRESSION    │      │  │ *idReco      INT │
     │  │    1:N       │    ├──────────────────┤      │  │  score_pert FLOAT│
     │  └──────────────┼───>│ *idProgression   │      └─>│  date_gen     DT │
     │                 │    │  pourcentage FLOAT│         │  statut  VARCHAR │
     │                 │    │  dern_activite DT │         │  idEtudiant  INT │──FK
     │                 │    │  idEtudiant  INT │──FK      │  idRessource INT │──FK
     │                 │    │  idCours     INT │──FK      └──────────────────┘
     │                 │    └──────────────────┘
     │                 │
     │   1:N           │    ┌──────────────────┐
     └─────────────────┼───>│   OBJECTIF_      │
                       │    │  APPRENTISSAGE   │
                       │    ├──────────────────┤
                       │    │ *idObjectif  INT │
                       │    │  description TEXT│
                       │    │  date_cible  DATE│
                       │    │  statut  VARCHAR │
                       │    │  idEtudiant  INT │──FK
                       │    └──────────────────┘
                       │
                       │    ┌──────────────────┐        ┌──────────────────┐
                       │    │   FORUM_POST     │        │   COMMENTAIRE    │
                       │    ├──────────────────┤        ├──────────────────┤
                       └───>│ *idPost      INT │───────>│ *idCommentaire   │
                            │  titre   VARCHAR │  1:N   │  contenu    TEXT │
                            │  contenu    TEXT │        │  date_creation DT│
                            │  date_creation DT│        │  idAuteur    INT │──FK
                            │  idAuteur    INT │──FK    │  idPost      INT │──FK
                            │  idCours     INT │──FK    └──────────────────┘
                            └──────────────────┘
```

### 8.3 Normalisation

Le modèle respecte la **3ème Forme Normale (3NF)** :

- **1NF** : Tous les attributs sont atomiques (pas de valeurs multiples ni de groupes répétitifs).
- **2NF** : Toutes les clés primaires sont simples (auto-incrémentées). Chaque attribut non-clé dépend entièrement de la clé primaire.
- **3NF** : Aucune dépendance transitive. Les informations de l'enseignant ne sont pas dupliquées dans la table COURS (on stocke uniquement `idEnseignant` comme clé étrangère).

### 8.4 Double base de données

| Base de données | Technologie | Usage |
|-----------------|-------------|-------|
| **SQL**         | PostgreSQL  | Utilisateurs, cours, quiz, progression, recommandations, objectifs, forum |
| **NoSQL**       | MongoDB     | Catalogue de ressources pédagogiques (vidéos, articles, fichiers), métadonnées de contenu, logs d'activité |

**Justification** : PostgreSQL assure l'intégrité relationnelle pour les données structurées (utilisateurs, scores, relations). MongoDB offre la flexibilité nécessaire pour stocker des ressources pédagogiques aux formats variés et les métadonnées associées au moteur de recommandation.

---

## 9. Architecture technique

### 9.1 Architecture microservices

```
┌─────────────────────────────────────────────────────────────────────────┐
│                          CLIENTS                                        │
│  ┌───────────────┐     ┌───────────────┐     ┌───────────────┐         │
│  │  Web (React)  │     │ Mobile (React │     │  Mobile (Flet)│         │
│  │               │     │   Native)     │     │               │         │
│  └───────┬───────┘     └───────┬───────┘     └───────┬───────┘         │
└──────────┼─────────────────────┼─────────────────────┼──────────────────┘
           │                     │                     │
           └─────────────────────┼─────────────────────┘
                                 │ HTTPS
                                 ▼
                    ┌────────────────────────┐
                    │     API Gateway        │
                    │   (Load Balancer)      │
                    └───────────┬────────────┘
                                │
           ┌────────────────────┼────────────────────┐
           │                    │                    │
           ▼                    ▼                    ▼
┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐
│  Auth Service    │ │  Cours Service   │ │  Reco Service    │
│  (FastAPI)       │ │  (FastAPI)       │ │  (FastAPI + ML)  │
│                  │ │                  │ │                  │
│ - Signup         │ │ - CRUD Cours     │ │ - Collaborative  │
│ - Login          │ │ - CRUD Modules   │ │   Filtering      │
│ - JWT            │ │ - CRUD Ressources│ │ - Content-Based  │
│ - Gestion rôles  │ │ - Recherche      │ │   Filtering      │
└────────┬─────────┘ └────────┬─────────┘ └────────┬─────────┘
         │                    │                    │
         │           ┌────────┼────────┐           │
         │           │        │        │           │
         ▼           ▼        │        ▼           ▼
┌──────────────────┐ │  ┌──────────────────┐ ┌──────────────┐
│  Progress        │ │  │  Social Service  │ │    Redis     │
│  Service         │ │  │  (FastAPI)       │ │   (Cache)    │
│  (FastAPI)       │ │  │                  │ └──────────────┘
│                  │ │  │ - Forum          │
│ - Suivi          │ │  │ - Commentaires   │
│ - Dashboard      │ │  │ - Notifications  │
│ - WebSocket      │ │  └──────────────────┘
└────────┬─────────┘ │
         │           │
         ▼           ▼
┌──────────────────────────────┐    ┌──────────────────┐
│        PostgreSQL            │    │     MongoDB       │
│  (Utilisateurs, Quiz,       │    │  (Ressources,     │
│   Progression, Forum)        │    │   Métadonnées,    │
│                              │    │   Logs)           │
└──────────────────────────────┘    └──────────────────┘
```

### 9.2 Stack technologique

| Couche          | Technologie                     | Justification                              |
|-----------------|---------------------------------|--------------------------------------------|
| Frontend Web    | React.js                        | Composants réutilisables, large écosystème |
| Frontend Mobile | React Native / Flet             | Code partagé avec le web / Python natif   |
| Backend API     | Python (FastAPI)                | Haute performance async, documentation auto|
| IA/ML           | scikit-learn, Surprise          | Filtrage collaboratif et content-based     |
| BDD relationnelle | PostgreSQL                   | Intégrité, performance, fiabilité         |
| BDD documents   | MongoDB                        | Flexibilité pour ressources variées       |
| Cache           | Redis                           | Performance des recommandations fréquentes |
| Temps réel      | WebSockets (FastAPI)            | Mise à jour instantanée progression       |
| Auth            | JWT (python-jose) + bcrypt      | Sécurité stateless                        |
| Conteneurs      | Docker                          | Isolation et portabilité des services     |
| Orchestration   | Kubernetes                      | Scalabilité et haute disponibilité        |
| CI/CD           | GitHub Actions                  | Automatisation déploiement                |
| Cloud           | AWS (EC2, RDS, S3) ou Azure     | Infrastructure managée et scalable        |
| Stockage objets | AWS S3 / Azure Blob Storage     | Stockage ressources à faible coût         |

### 9.3 Infrastructure de déploiement

```
┌─────────────────────────────────────────────────────────┐
│                    Cloud (AWS / Azure)                   │
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │              Kubernetes Cluster                   │   │
│  │                                                   │   │
│  │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌────────┐│   │
│  │  │Auth Pod │ │Cours Pod│ │Reco Pod │ │Social  ││   │
│  │  │(Docker) │ │(Docker) │ │(Docker) │ │Pod     ││   │
│  │  └─────────┘ └─────────┘ └─────────┘ └────────┘│   │
│  │                                                   │   │
│  │  ┌─────────┐ ┌──────────────────────────────┐   │   │
│  │  │Progress │ │      Ingress Controller      │   │   │
│  │  │Pod      │ │      (Load Balancer)         │   │   │
│  │  └─────────┘ └──────────────────────────────┘   │   │
│  │                                                   │   │
│  └─────────────────────────────────────────────────┘   │
│                                                         │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐             │
│  │ RDS      │  │ MongoDB  │  │ S3/Blob  │             │
│  │(Postgres)│  │ Atlas    │  │ Storage  │             │
│  └──────────┘  └──────────┘  └──────────┘             │
│                                                         │
│  ┌──────────┐  ┌──────────────────────────┐            │
│  │ Redis    │  │ GitHub Actions (CI/CD)   │            │
│  │(ElastiC.)│  └──────────────────────────┘            │
│  └──────────┘                                           │
└─────────────────────────────────────────────────────────┘
```

---

## 10. Défis et solutions

### Défi 1 : Précision des recommandations personnalisées

**Problème** : Les modèles de recommandation pourraient fournir des résultats non pertinents ou trop généralistes.

**Solutions** :
- Combiner le **filtrage collaboratif** (basé sur les comportements d'étudiants similaires) avec le **filtrage basé sur le contenu** (basé sur les caractéristiques des ressources).
- Intégrer un **système de feedback** permettant aux étudiants de noter la pertinence des recommandations.
- Gérer le problème du **cold start** (nouveaux utilisateurs) via un questionnaire de profil initial et des recommandations basées sur la popularité.

### Défi 2 : Gestion des données utilisateurs et vie privée

**Problème** : La collecte de données personnelles liées à l'apprentissage soulève des préoccupations de vie privée.

**Solutions** :
- Mécanismes de **consentement explicite** (opt-in) pour la collecte des données.
- Chiffrement des mots de passe avec **bcrypt** et des données sensibles en transit (HTTPS/TLS).
- Conformité **RGPD** : droit à l'oubli, portabilité, minimisation des données.
- Tokens **JWT** avec expiration configurable (60 min par défaut).

### Défi 3 : Scalabilité des services de recommandation

**Problème** : Le traitement des recommandations pour de nombreux utilisateurs simultanément peut poser des problèmes de performance.

**Solutions** :
- **Redis** pour mettre en cache les recommandations fréquentes et limiter les charges sur les bases de données.
- Architecture **Kubernetes** avec autoscaling horizontal pour le service de recommandation.
- Calcul des recommandations en **batch asynchrone** (pré-calcul périodique) plutôt qu'en temps réel pour les cas non critiques.

### Défi 4 : Suivi de la progression en temps réel

**Problème** : Les utilisateurs doivent suivre leur progression instantanément.

**Solutions** :
- **WebSockets** (intégrés à FastAPI) pour les mises à jour en temps réel du tableau de bord.
- Triggers en base de données pour ajuster automatiquement les recommandations selon la progression.

### Défi 5 : Coût du stockage de ressources pédagogiques massives

**Problème** : Le stockage de vidéos, articles et fichiers peut engendrer des coûts élevés.

**Solutions** :
- Utilisation de **AWS S3 / Azure Blob Storage** pour le stockage objet à faible coût.
- Politique de **cycle de vie** des données : archivage des anciennes ressources, suppression des redondances.
- **CDN** (CloudFront / Azure CDN) pour la distribution performante des contenus.

---

## 11. Calendrier prévisionnel

| Semaine | Activités                                                                                     |
|---------|-----------------------------------------------------------------------------------------------|
| **S1**  | Collecte des exigences, conception de l'architecture microservices, modélisation des données   |
| **S2**  | Mise en place du frontend (React / React Native) et du backend (API FastAPI, base de données) |
| **S3**  | Intégration des modèles de recommandation IA, configuration PostgreSQL + MongoDB               |
| **S4**  | Conteneurisation des microservices avec Docker, orchestration avec Kubernetes                   |
| **S5**  | Mise en place du pipeline CI/CD (GitHub Actions), déploiement cloud (AWS / Azure)              |
| **S6**  | Tests (unitaires, intégration, charge), corrections, finalisation documentation, présentation  |

---

## Annexe A : État actuel de l'implémentation

Le microservice d'authentification est déjà implémenté avec :

- **Framework** : FastAPI (Python)
- **Endpoints** : `POST /auth/signup` et `POST /auth/login`
- **Sécurité** : Hashage bcrypt, tokens JWT (HS256, expiration 60 min)
- **Base de données** : SQLite (développement), compatible PostgreSQL (production)
- **Modèle** : Table `Utilisateur` avec rôles (Étudiant, Enseignant, Admin)
- **Validation** : Pydantic (EmailStr, longueur min/max)
- **Scripts SQL** : Disponibles pour MySQL, PostgreSQL et SQL Server

### Endpoints existants

| Méthode | Route           | Description                          | Requête                                           | Réponse               |
|---------|-----------------|--------------------------------------|---------------------------------------------------|-----------------------|
| POST    | `/auth/signup`  | Créer un compte utilisateur          | `{nom, email, mot_de_passe, role}`                | `{access_token}`      |
| POST    | `/auth/login`   | Se connecter                         | `{email, mot_de_passe}`                           | `{access_token}`      |

---

## Annexe B : Modèles de recommandation

### Filtrage collaboratif
Analyse les comportements et préférences d'étudiants similaires pour recommander des ressources qu'un étudiant n'a pas encore consultées. Si l'étudiant A et l'étudiant B ont des parcours similaires et que B a apprécié une ressource que A n'a pas vue, cette ressource sera recommandée à A.

### Filtrage basé sur le contenu
Analyse les caractéristiques des ressources déjà consultées et appréciées par l'étudiant (catégorie, type, niveau de difficulté, mots-clés) pour recommander des ressources aux caractéristiques similaires.

### Approche hybride
La plateforme combine les deux approches pour maximiser la pertinence :
1. Score collaboratif + Score contenu → Score final pondéré
2. Le poids de chaque composante s'ajuste automatiquement en fonction du volume de données disponibles pour chaque étudiant.

---

*Document généré dans le cadre du projet de Plateforme Éducative Intelligente.*
