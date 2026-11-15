# Guide Détaillé : Canaux Alpha RGBA & Décomposition en Calques (Layerization)

## 1. Génération Natif de Canaux Alpha (Transparence RGBA)
Seedream 5.5 génère nativement des fichiers PNG à 4 canaux avec semi-transparence et anti-crénelage parfait des bordures.

### Alignment Technique & Sémantique
- **Réglages API obligatoires** :
  - `background`: `transparent`
  - `output_format`: `png`
- **Règle de Rédaction (Isolement)** :
  - Ne **jamais** décrire d'environnement ou de décor dans le prompt (pas de table, pas de néon) sous peine de dissonance cognitive.
  - Centrer la silhouette dans un espace sémantiquement vide.
- **Exemple Optimal** :
  *"Un autocollant découpé d'un panda roux endormi étreignant un coussin en forme de croissant. Utiliser des formes plates corail, anthracite et crème. Centrer la silhouette complète avec un espace vide généreux tout autour. Sortie RGBA avec un espace transparent autour du personnage."*

### Limite des Matériaux Translucides (Verre)
Les volumes en verre (ex: bouteille de parfum) avec `background: transparent` peuvent conserver un corps opaque à l'intérieur.
- **Solution** : Générer l'objet sur fond opaque de studio, puis utiliser des modes de fusion (Blending Modes comme "Produit" ou "Écran") dans Photoshop / After Effects.

---

## 2. Décomposition en Calques (Layer Decomposition & Rich-Text OCR)
Permet de décomposer une image plate unique en un maximum de 99 calques PNG transparents + une image de fond in-painted (`z_index: 0`).

### Métadonnées JSON Renvoyées
- `data[].z_index` : Ordre d'empilement (0 pour l'arrière-plan reconstitué, 1..N pour les calques).
- `bounding_box.normalized` : Coordonnées normalisées (0 à 1000) permettant de repositionner le calque sur n'importe quel canevas responsive.
- `bounding_box.absolute` : Coordonnées en pixels réels.

### Guidage de la Décomposition (Steering the Split)
- **Séparation Sémantique** : *"Isoler le disque vinyle, son étiquette centrale, la pochette de l'album et le plateau du tourne-disque."*
- **Séparation Géospatiale** : *"Séparer les régions aux coordonnées 308 484 438 570 et 566 484 694 570 en deux calques distincts."*

### Extraction Typographique Avancée (Rich-Text OCR)
En activant `text_recognition: true`, l'API renvoie :
- Le texte brut et les coordonnées de chaque ligne.
- L'objet `style` : `similar_font_family`, `foreground_color` (`#RRGGBB`), et les booléens (`bold`, `italic`, `underline`, `shadow`).
- Permet l'automatisation complète de la localisation marketing multilingue.
