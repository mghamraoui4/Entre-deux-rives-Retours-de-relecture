# Entre deux rives — Page de relecture
 
Page web qui permet aux 4 relecteurs de la **version de correction 2** (147 pages) d'envoyer leurs corrections et leur avis global. Les retours arrivent dans une feuille Google.
 
## Les fichiers
 
| Fichier | Rôle |
|---|---|
| `index.html` | La page de relecture, hébergée sur GitHub Pages. |
| `Code.gs` | Le script Apps Script qui reçoit les envois et les écrit dans la feuille Google. |
| `LISEZMOI.md` | Ce mode d'emploi. |
 
## Fonctionnement
 
```
Relecteur  →  index.html (GitHub Pages)  →  Code.gs (Apps Script)  →  Feuille Google
```
 
- Le relecteur note ses corrections au fil de la lecture. Elles restent enregistrées sur son appareil, même s'il ferme la page.
- Un bouton envoie toute sa liste en une fois.
- À la fin, il remplit l'onglet **Avis global**.
- Tant que l'URL du script n'est pas renseignée, ou si l'envoi échoue, la page propose de **copier le texte** pour l'envoyer à la main (WhatsApp, e-mail).
## Mise en place (environ 10 minutes)
 
### 1. La feuille Google
 
1. Crée une feuille Google vide, nommée **« Entre deux rives — Relecture »**.
2. Ouvre **Extensions → Apps Script**, efface le code existant, colle le contenu de `Code.gs`, puis enregistre.
3. Dans la barre du haut, choisis la fonction **`setupSheet`**, clique sur **Exécuter** et accepte les autorisations. Le script crée trois onglets : **Corrections**, **Avis** et **Synthèse**.
4. Ouvre **Déployer → Nouveau déploiement**, choisis le type **Application Web**, puis règle :
   - *Exécuter en tant que :* **Moi**
   - *Qui a accès :* **Tout le monde**
5. Copie l'URL qui se termine par **`/exec`**.
### 2. La page
 
1. Ouvre `index.html` et repère la ligne :
```js
const SCRIPT_URL = "COLLE_ICI_L_URL_APPS_SCRIPT";
```
   Remplace `COLLE_ICI_L_URL_APPS_SCRIPT` par l'URL copiée.
2. Dans le dépôt GitHub `entre-deux-rives-retours`, choisis **Add file → Upload files** et dépose `index.html` dans un dossier `relecture/`.
3. Après une à deux minutes, la page est en ligne à l'adresse :
   **`https://mghamraoui4.github.io/entre-deux-rives-retours/relecture/`**
 
### 3. Tester avant d'envoyer le lien
 
1. Ouvre la page, saisis un prénom, ajoute une fausse correction et clique sur **Envoyer**.
2. Vérifie qu'une ligne apparaît dans l'onglet **Corrections** (cela prend quelques secondes).
3. Supprime cette ligne de test, puis envoie le lien à tes 4 relecteurs.
## La feuille Google
 
### Onglet « Corrections »
 
Une ligne par correction : date, relecteur, page, type, importance, passage, proposition, **statut**.
 
- La colonne **Statut** propose un menu déroulant : *À traiter*, *Corrigé*, *Refusé*, *À discuter*. Mets-la à jour au fur et à mesure.
- Les lignes **bloquantes** sont surlignées en rouge, celles **à corriger** en jaune. Les lignes **corrigées** passent en gris.
- Un filtre est activé sur les en-têtes. Pour commencer par l'essentiel, filtre **Importance = Bloquante** et **Statut = À traiter**.
- La colonne **Lot** est masquée : elle sert seulement à éviter les doublons.
### Onglet « Avis »
 
Un avis par relecteur : note, facilité de lecture, titre, recommandation, passages marquants, passages trop longs, passages sensibles, dernier mot. Si un relecteur renvoie un avis modifié, sa ligne est **remplacée**.
 
### Onglet « Synthèse »
 
- Les totaux : corrections reçues (bloquantes, à corriger, mineures), corrections restant à traiter, bloquantes à traiter.
- Les avis : nombre reçu, note moyenne, lecture moyenne, nombre de relecteurs qui recommandent le livre.
- Le tableau par relecteur : nombre de corrections, nombre de bloquantes, avis envoyé ou non.
## Sécurité
 
- **Champ piège anti-robots :** un envoi qui le remplit est ignoré.
- **Formules neutralisées :** un texte qui commence par `=`, `+`, `-` ou `@` est écrit tel quel, sans être exécuté.
- **Pages contrôlées :** seules les pages de 1 à 147 sont acceptées.
- **Pas de doublons :** un même lot renvoyé après une coupure n'est jamais écrit deux fois.
- **Discrétion :** la page n'apparaît pas dans les moteurs de recherche (`noindex`). Seuls ceux qui ont le lien peuvent y accéder.
## À savoir
 
- **Chaque relecteur doit garder le même appareil et le même navigateur** jusqu'à l'envoi, puisque sa liste y est stockée. S'il change d'appareil, il doit d'abord envoyer ce qu'il a noté.
- **Si tu modifies `Code.gs` :** ouvre **Déployer → Gérer les déploiements → Modifier (crayon) → Version : Nouvelle version → Déployer**. Sinon, l'ancienne version reste en ligne.
- **Si une formule de « Synthèse » affiche `#ERROR!` :** relance `setupSheet`. L'onglet Synthèse est recréé, et les onglets Corrections et Avis ne sont pas touchés.
- **Pour changer le nombre de pages :** modifie `MAX_PAGE` dans `index.html` **et** dans `Code.gs`, puis redéploie le script.
 
