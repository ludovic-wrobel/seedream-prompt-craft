# Guide Détaillé : La Règle des 5 Piliers Descriptifs pour Seedream 5.5

Ce document fournit la méthodologie complète pour la rédaction de prompts Text-to-Image ex nihilo sur Seedream 5.5.

## Pourquoi l'abandon du Bag-of-Words ?
Seedream 5.5 s'appuie sur une compréhension linguistique profonde guidée par LLM. Les listes de mots-clés ("bag-of-words") séparés par des virgules détruisent les relations hiérarchiques et la conscience spatiale du modèle, provoquant des confusions et des fusions d'objets ("object blending").

## Les 5 Piliers d'un Prompt Parfait

### 1. Le Livrable et sa Fonctionnalité ("Job-to-be-done Prompting")
Conditionne le modèle sur le métier et la mise en page.
- **Exemples** :
  - *"Une affiche de cinéma verticale pour..."*
  - *"Une photographie de produit héroïque pour un catalogue e-commerce..."*
  - *"Un autocollant découpé de..."*
  - *"Un menu de café compact..."*

### 2. Le Sujet, l'Action et les Attributs Factuels
Décrire la scène centrale sous forme de phrase complète : Sujet + Verbe + Complément.
- **Incorrect** : *chat, roux, fenêtre, pluie, aquarelle*
- **Optimal** : *Un chat roux enroulé sur une banquette près d'une fenêtre pendant que la pluie coule sur la vitre.*

### 3. L'Environnement et le Placement Spatial
Seedream 5.5 cartographie l'espace en liant chaque objet à une surface ou un voisin avec des prépositions de lieu.
- **Exemple** : *"Des engrenages en laiton sont éparpillés sur un tapis en cuir vert, une loupe repose sur une montre de poche ouverte, des pinces se dressent dans une petite tasse en céramique à côté d'une boîte d'huile."*

### 4. La Lumière, la Caméra et les Matériaux
Exploite le moteur de rendu physique (évite les peaux cireuses "waxy skin" et les reflets excessifs).
- **Exemple** : *"Lumière du jour froide provenant de la gauche avec une faible lueur chaude en arrière-plan. Grain de pellicule 35mm. Plan rapproché à hauteur de taille avec une faible profondeur de champ, l'arrière-plan étant doucement flouté. Texture de peau naturelle avec des pores visibles."*

### 5. Les Contraintes et Exclusions Organiques
Comme il n'y a pas de champ Negative Prompt dans l'API, les exclusions sont rédigées en prose à la fin du prompt.
- **Exemples** :
  - *"Ne pas inclure de texte, de logos ou de mains."*
  - *"Exclure tout personnage dans la rue et tout effet 3D."*
  - *"Aucune ligne de croquis visible."*
