# Guide Détaillé : Édition Itérative (Multi-Round) & Fusion Multi-Images

## 1. Édition Itérative (Multi-Round Editing : Méthodologie State & Delta)
Seedream 5.5 permet de réaliser plus de 100 cycles d'édition consécutifs sans dérive visuelle (color drift), grâce à sa préservation au niveau du pixel.

### Structure d'une Requête d'Édition (Cycle N+1)
L'image approuvée du cycle N doit être fournie dans le paramètre API `images` / `image_urls`.

1. **Le Delta (Changement Ciblé)** :
   - Une seule modification par cycle (ex: changer le vêtement au cycle 1, l'arrière-plan au cycle 2).
   - Nommer précisément la cible sans pronoms vagues ("ça", "celui-ci").
   - *Exemple* : *"Changer uniquement la veste jaune de la femme pour une version bleu cobalt profond de la même veste."*
2. **La Frontière de Préservation (Boundary Explicite)** :
   - Dicter textuellement toutes les zones à geler pour renforcer le vecteur d'attention du modèle.
   - *Exemple* : *"Préserver la coupe du vêtement, les plis et la texture du tissu. Garder son identité faciale, sa coiffure, son expression, sa pose et les accessoires inchangés. Préserver le bâtiment, la direction de la lumière et la perspective de la caméra."*
3. **L'Intégration d'Éclairage** :
   - *Exemple* : *"La nouvelle couleur doit suivre les reflets et les ombres du tissu existant."*

---

## 2. Fusion Multi-Images (Multi-Image Fusion avec Balises @)
Seedream 5.5 supporte jusqu'à 10 images de référence simultanées (`images: [@image1, @image2, ...]`).

### Règles d'Ancrage et de Cartographie des Rôles
Chaque image doit recevoir un rôle exclusif dans le prompt textuel pour éviter le mélange chaotique de styles et de formes.

- **Procédure** :
  1. Identifier le rôle de chaque référence.
  2. Rédiger le prompt avec les balises `@image1`, `@image2`, etc.
- **Exemple de Syntax Optimal** :
  *"Mettre la femme de @image1 dans la veste de @image2, debout dans la gare de @image3. Garder le visage, la coiffure et l'expression de la femme exactement comme dans @image1. Garder la couleur, la matière et les coutures de la veste exactement comme dans @image2. Lumière du matin filtrant à travers les fenêtres de la gare, look de pellicule 35mm."*
