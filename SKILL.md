---
name: seedream-prompt-craft
display_name: Seedream 5.5 Prompt Engineering & Visual Workflow
version: 1.0.0
description: "Ingénierie de prompts et configuration de pipelines visuels déterministes pour le modèle génératif Seedream 5.5 (ByteDance Seed)."
author: Gemini Notebook
triggers:
  - seedream
  - seedream 5.5
  - prompt seedream
  - génération image seedream
  - édition image seedream
  - transparence rgba
  - décomposition calques
---

# Skill : Seedream 5.5 Prompt Crafting & API Workflow Guide

## 🎯 Directives pour l'Agent (When & How to Use)

### Conditions de Déclenchement
Invoquez ce skill dès que l'utilisateur demande :
1. De rédiger, optimiser ou corriger un prompt pour **Seedream 5.5**.
2. De configurer une requête API (résolution, ratio, arrière-plan, format de sortie, références).
3. De réaliser un workflow de **retouche itérative (Multi-Round Editing)** sans dérive visuelle.
4. De combiner plusieurs images de référence (**Multi-Image Fusion** avec balises `@`).
5. De générer un objet détouré à fond transparent (**Canal Alpha RGBA natif**).
6. De décomposer une image en calques autonomes ou d'effectuer une extraction typographique (**Layer Decomposition & OCR**).

### Instructions d'Exécution pas-à-pas pour l'Agent
1. **Déterminer le Mode Opératoire** :
   - `Text-to-Image` (Génération ex nihilo)
   - `Multi-Round Editing` (Modification séquentielle N+1)
   - `Multi-Image Fusion` (Assemblage avec balises `@image1`, `@image2`)
   - `RGBA Transparency` (Détourage natif)
   - `Layer Decomposition` (Découpage en calques / OCR)
2. **Séparer Strictement API et Prose** :
   - Placer les contraintes spatiales et techniques (`resolution`, `aspect_ratio`, `background`, `output_format`) dans la configuration API.
   - **Interdiction absolue** de mettre des mots-clés techniques ("16:9", "4K", "HD", "8K") dans le texte du prompt.
3. **Appliquer la Règle des 5 Piliers Descriptifs** :
   - Formuler des phrases déclaratives complètes (Sujet + Verbe + Complément).
   - Bannir le "bag-of-words" (listes de mots-clés séparés par des virgules) et les adjectifs vagues ("magnifique", "époustouflant").
4. **Formater les Textes Typographiques** :
   - Encadrer le texte littéral entre guillemets doubles stricts (ex: `"NIGHT GARDEN"`).
   - Toujours ajouter la clause d'exclusion textuelle : `"N'inclure aucun autre texte"`.
5. **Fournir le Résultat structuré** :
   - Fournir la **Configuration API JSON**.
   - Fournir le **Prompt Textuel Optimisé**.
   - Expliquer brièvement la justification sémantique.

---

## 🏗️ Architecture Technique et Principes Fondamentaux

### Paradigme Déterministe vs Diffusion Probabiliste
Seedream 5.5 (déployé par ByteDance Seed le 9 novembre 2026) fonctionne comme un **moteur d'assemblage modulaire déterministe**. Contrairement aux anciens modèles probabilistes, il garantit :
- Une **préservation au niveau du pixel** sur plus de 100 cycles d'édition itérative.
- La génération native d'un **canal alpha à 4 canaux (RGBA)**.
- Un rendu typographique multilingue avec un taux de corruption grave de seulement 0.4%.
- La **décomposition d'images plates** jusqu'à 99 calques PNG transparents avec coordonnées géospatiales.

---

## ⚙️ Configuration des Paramètres API

| Paramètre API | Valeurs Supportées | Règle & Usage |
| :--- | :--- | :--- |
| `resolution` / `size` | `1K`, `1.5K`, `2K`, `3K`, `auto` | `2K` par défaut (standard industrial). `3K` pour texte dense/haute fidélité. `auto` pour conserver la taille d'origine lors d'une édition (max 4.62 MP). |
| `aspect_ratio` | `1:1`, `16:9`, `9:16`, `3:2`, `2:3`, `4:3`, `3:4`, `21:9` | Détermine le format du canevas. Laisser vide en édition pour conserver le ratio de la 1ère référence. |
| `background` | `auto`, `transparent`, `opaque` | `transparent` force le canal alpha RGBA. `opaque` est recommandé pour les chaînes d'édition afin d'éviter la dérive des couleurs. |
| `output_format` | `png`, `jpeg` | `png` **strictement obligatoire** quand `background: transparent`. |
| `images` / `image_urls` | Tableau d'URL (Max 10 images) | Max 30 Mo par fichier. Associé aux balises `@image1`, `@image2` dans le prompt. |

---

## 📐 La Règle des Cinq Piliers Descriptifs (Text-to-Image)

1. **Le Livrable et sa Fonctionnalité ("Job-to-be-done")** : Définir la nature exacte ("Une affiche de cinéma pour...", "Une photographie de produit héroïque pour...").
2. **Le Sujet, l'Action et les Attributs Factuels** : Description en phrases complètes (Sujet + Verbe + Complément).
3. **L'Environnement et le Placement Spatial** : Prépositions de lieu précises pour ancrer chaque objet ("sur", "à côté de", "dans la partie supérieure").
4. **La Lumière, la Caméra et les Matériaux** : Direction et température de la lumière, type d'objectif (ex: pellicule 35mm, faible profondeur de champ, texture de peau naturelle sans effet cireux).
5. **Les Contraintes et Exclusions Organiques** : Formuler l'exclusion en dernière phrase ("Ne pas inclure de texte...", "Exclure les personnages..."). Pas de champ Negative Prompt séparé.

---

## 🔤 Rendu Typographique & Textes Multilingues

- **Guillemets Doubles Stricts** : Tout texte à imprimer doit être entre guillemets doubles (ex: `"PALAIS D'AMBRE"`).
- **Concision** : Se limiter aux titres, sous-titres, prix ou dates. Pas de paragraphes longs.
- **Clause Anti-Hallucination** : Toujours inclure *"N'inclure aucun autre texte"*.
- **Topologie complète** : Spécifier la chaîne + le style/script (ex: calligraphie thuluth pour l'arabe, mincho vertical pour le japonais) + l'emplacement spatial + la couleur.

---

## 🔄 Édition Itérative (Multi-Round Editing : State & Delta)

Pour modifier une image d'un cycle N à N+1 sans dérive visuelle :
1. **Delta (Changement ciblé)** : Nommer précisément l'élément et l'unique modification demandée (1 seul changement par cycle).
2. **Boundary (Frontière de préservation)** : Détailler explicitement tout ce qui doit rester gelé ("Préserver l'identité faciale, la pose, la coiffure, l'arrière-plan, la lumière et la caméra").
3. **Intégration d'éclairage** : Ordonner d'adapter les ombres et reflets du nouvel élément à l'éclairage ambiant.
4. **Ré-injection d'image** : Utiliser l'image approuvée du cycle N dans le paramètre `image_urls`.

---

## 🔀 Fusion Multi-Images (Balises @)

Lors de l'utilisation de plusieurs images d'entrée (jusqu'à 10) :
- Assigner un rôle exclusif à chaque image avec `@image1`, `@image2`, etc.
- Exemple : *"Mettre la femme de @image1 dans la veste de @image2, debout dans la gare de @image3. Garder le visage de @image1 et la couleur/texture de la veste de @image2."*

---

## ✂️ Canaux Alpha (RGBA Natif) & Décomposition en Calques

### Transparence RGBA
- Réglages API : `background: transparent` + `output_format: png`.
- Prompt : Isoler l'entité. **Interdiction de décrire un environnement** (pas de table, pas de décor) pour éviter la dissonance cognitive.
- Note verre/translucide : Si le corps en verre reste opaque, utiliser le mode opaque + studio et blending modes en post-production.

### Layer Decomposition (Décomposition en Calques)
- Endpoint / Paramètre : `layer_decomposition: true`, `max_images`: 2 à 100 (défaut 30).
- Métadonnées renvoyées : `z_index` (0 = fond in-painted, 1..N = calques), `bounding_box.normalized` (0 à 1000 pour le design responsive).
- Option OCR : `text_recognition: true` renvoie le texte brut, les polices similaires, la couleur `#RRGGBB` et le style (`bold`, `italic`, etc.).

---

## 📋 Tableau Synthétique des Do's and Don'ts

| Catégorie | À Faire (Do's) | À Éviter (Don'ts) |
| :--- | :--- | :--- |
| **Structure** | Phrases déclaratives complètes avec prépositions spatiales. | Empiler des mots-clés ("cyberpunk, 8k, masterpiece"). |
| **Technique** | Configurer `aspect_ratio` et `resolution` via l'API. | Écrire "16:9" ou "4K" dans le texte du prompt. |
| **Texte** | Encadrer avec `" "` et ajouter "N'inclure aucun autre texte". | Demander d'ajouter un texte sans guillemets ni emplacement. |
| **Édition** | 1 modification par cycle + clause Boundary explicite. | Demander "d'améliorer l'image" sans lister ce qui est gelé. |
| **Transparence**| `background: transparent` + `png` + sujet isolé sans décor. | Décrire un décor ("sur une table") avec `transparent`. |
