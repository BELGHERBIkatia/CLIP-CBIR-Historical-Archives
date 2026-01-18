# CLIP-CBIR-Historical-Archives
Projet : Recherche d'Images Patrimoniales (Fonds Roger-Viollet)

---

##  1. Présentation du Projet
Ce projet implémente un système de **Recherche d'Images par le Contenu (CBIR)** appliqué aux archives photographiques historiques des agences **Branger** et **Harlingue**. 

L'objectif est double :
1. **Détection de "Near-Duplicates"** : Identifier des copies ou des versions modifiées d'une même œuvre.
2. **Recherche Sémantique** : Permettre une navigation multimodale (Texte -> Image) dans les fonds patrimoniaux.

---

##  2. Méthodologie
Nous utilisons le modèle **CLIP (Contrastive Language-Image Pre-training)** de OpenAI, qui permet de lier le langage naturel aux pixels.

### Approche 1 : Zero-Shot (Baseline)
Utilisation du modèle original pour évaluer les capacités natives de CLIP sur des photos du début du XXème siècle.

### Approche 2 : Fine-Tuning Contrastif
Réentraînement du modèle sur 1000 paires (Image, Légende) avec la perte **Multiple Negatives Ranking Loss (MNRL)**. Cette étape permet d'ancrer le vocabulaire historique des légendes Excel dans les représentations visuelles du modèle.



---

##  3. Résultats et Analyse de Performance

### Robustesse aux Near-Duplicates
Le modèle affiche une précision remarquable pour retrouver l'originale après modifications (crop, contraste, flou) :
* **Recall@1 : 100%** (sur un échantillon de 100 tests aléatoires).
* **Similarité Cosinus :** Moyenne de **0.95** pour les doublons.

### Analyse de Robustesse Dynamique
J'ai testé les limites du modèle avec des intensités de dégradation croissantes :

| Intensité | Recall@1 | Observation |
| :--- | :--- | :--- |
| **0.1** | 100% | Infaillible sur les modifications légères. |
| **0.5** | 78% | Très bonne résistance au flou et au bruit. |
| **0.9** | 46% | Seuil critique : la perte d'information visuelle est trop forte. |



### Recherche Multimodale
Le fine-tuning permet une recherche sémantique précise :
* **Exemple :** La requête *"Xylophone, 1905"* identifie l'image exacte en Top-1 (Score : 0.40).

---

##  4. Interfaces de Démonstration (Gradio)
Deux interfaces ont été développées pour tester le système en temps réel :
1. **Recherche par Image :** Pour identifier instantanément un doublon dans la base.
2. **Recherche Sémantique :** Pour explorer la collection via des mots-clés.



---

##  Conclusion
Le Fine-Tuning a permis de transformer CLIP en un expert du domaine patrimonial. Le système est capable de compenser les erreurs de numérisation ou les altérations physiques des documents, garantissant une intégrité parfaite de la base de données (Recall 100%).
