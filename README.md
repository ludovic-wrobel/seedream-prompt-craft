# 🎨 Seedream 5.5 Prompt Engineering & Visual Workflow Skill

Un skill agentique complet pour la conception de prompts optimisés et le paramétrage déterministe de l'API **Seedream 5.5** (développé par ByteDance Seed).

> 💡 **Crédits & Méthodologie** : Ce skill suit rigoureusement la méthode de génération de prompts et de workflows visuels pour **Seedream 5.5** développée par **Ludovic Wrobel**.

---

## 📌 Présentation

Ce skill fournit à tout agent IA (ou assistant guidé) les règles d'ingénierie sémantique, la structure spatiale et les schémas JSON API requis pour exploiter l'ensemble des capacités avancées du modèle Seedream 5.5.

### 🌟 Fonctionnalités prises en charge

- **Text-to-Image (Règle des 5 Piliers)** : Construction de prompts descriptifs en phrases déclaratives complètes (Job-to-be-done, Sujet & Action, Emplacement spatial, Lumière & Caméra, Exclusions organiques en prose).
- **Rendu Typographique Multilingue** : Intégration de texte sans hallucination de glyphes (arabe, chinois, japonais, cyrillique, latin) avec guillemets doubles et clause d'exclusion textuelle.
- **Édition Itérative (Multi-Round Editing)** : Méthodologie *State & Delta* garantissant la préservation stricte au niveau du pixel sur plus de 100 cycles consécutifs sans dérive visuelle.
- **Fusion Multi-Images** : Assemblage de 2 à 10 images de référence via des balises d'ancrage (`@image1`, `@image2`, etc.) et une cartographie stricte des rôles.
- **Transparence Native (Canal Alpha RGBA)** : Configuration du canal alpha à 4 canaux (`background: transparent`, `output_format: png`) et isolement sémantique sans décor.
- **Décomposition en Calques (Layer Decomposition & Rich-Text OCR)** : Découpage d'images plates jusqu'à 99 calques PNG transparents avec coordonnées géospatiales et extraction typographique stylisée.

---

## 📁 Structure du Dépôt

```text
seedream-prompt-craft/
├── README.md               # Documentation générale et guide d'installation GitHub
├── SKILL.md                # Guide d'instruction principal et règles pour l'agent IA
├── skill.json              # Manifeste du skill, déclencheurs (triggers) et schéma API
└── references/             # Guides techniques d'approfondissement
    ├── 5_piliers_prompting.md # Ingénierie Text-to-Image (Règle des 5 piliers)
    ├── edition_et_fusion.md   # Multi-round editing (State & Delta) et balises @
    └── rgba_et_calques.md     # Transparence RGBA natif & Décomposition en calques (OCR)
```

---

## ⚙️ Spécifications des Paramètres API

| Paramètre API | Valeurs autorisées | Description & Usage |
| :--- | :--- | :--- |
| `resolution` | `1K`, `1.5K`, `2K`, `3K`, `auto` | `2K` par défaut. `3K` pour texte dense ou macro. `auto` en édition. |
| `aspect_ratio` | `1:1`, `16:9`, `9:16`, `3:2`, `2:3`, `4:3`, `3:4`, `21:9` | Détermine le format du canevas horizontal/vertical. |
| `background` | `auto`, `transparent`, `opaque` | `transparent` force la génération du canal alpha RGBA. |
| `output_format` | `png`, `jpeg` | `png` **obligatoire** en mode fond transparent. |
| `images` | Tableau d'URL (Max 10) | Images de référence associées aux balises `@image1`, `@image2`... |

---

## 🚀 Installation & Utilisation

### Pour un Agent IA (Gemini / Claude / Custom Agent)
1. Téléchargez ou clonez ce dépôt dans le répertoire des skills de votre agent.
2. Déclenchez le skill lors d'une interaction en utilisant l'un des mots-clés d'activation (`seedream`, `seedream 5.5`, `prompt seedream`, `multi-round editing`, etc.).
3. L'agent consultera `SKILL.md` et les fichiers dans `references/` pour formuler le JSON API et le prompt textuel optimisé.

---

## 📜 Licence & Attribution

Ce projet est partagé sous licence open-source. La méthodologie de prompting et l'ingénierie visuelle Seedream 5.5 s'appuient sur les travaux et recommandations de **Ludovic Wrobel**.
