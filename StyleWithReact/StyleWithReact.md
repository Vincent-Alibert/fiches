---
title: StyleWithReact
---

# Objectif de la réunion

::: incremental

- Le style dans React
- Utilité de SASS et comment l'utilisé
- Le fichier variables.scss et mixins.scss
- Les médias queries

:::

# Le style dans React

::: incremental

- Inline CSS
- CSS in JS
- Styled Components
- CSS Modules
- Sass & SCSS
- etc.

:::

## Inline CSS

### Positif

- jamais obsolète
- Syntaxe classique

### Problème

- Pas la possibilité d'avoir un compilateur pour la compatibilité crossplatform
- Impossible d'utiliser les media queries

---

## CSS in JS et Styled Components

### Positif

- Manipulation assez facile du style
- Syntaxe assez proche du css

### Problème

- Obligation d'import de dépendances supplémentaires pour le fonctionnement et
  pour les medias queries
- Aprrendre une nouvelle méthode pour faire style

---

## CSS Modules

### Positif

- Css classique
- Possibilité de le compilité pour le rendre compatible cross platform
- Pas la peine d'apprendre le fonctionnement de dépendance supplémentaires
- Possibilité d'utiliser les media queries

### Problème

- On répète pas mal de css ici et là ce qui entraine une perte de temps à la
  terme

---

## Sass & SCSS

### Positif

- Css classique
- Possibilité de le compiler pour le rendre compatible cross platform
- Pas la peine d'apprendre le fonctionnement de dépendance supplémentaires
- Possibilité d'utiliser les media queries
- Possibilité de créer des fonctions (mixin), des variables et de les importer
  pour les réutiliser

---

### Problème

- Obligation d'import de dépendances supplémentaires pour le fonctionnement

# Le fonctionnement du css avec React

::: incrementale

- CRA ajoute dans le head
- Selon les lib (on montage et démontage)

:::

# Pourquoi SASS

::: incrementale

- La syntaxe est pratique
- Variables
- Fonctions (mixin)

:::

## Le fichier Variable

## Le fichier mixins

## Comment les utiliser

## Comment les mettres à jours ?

## Les médias queries

## L'attribut media peut prendre (depuis CSS2) les valeurs suivantes :

---

- screen
  - Écrans
- handheld
  - Périphériques mobiles ou de petite taille
- print
  - Impression
- tv
  - Téléviseur
- all
  - Tous les précédents

---

mais pas que... braille, embossed, projection, tty, aural

### Utilisation

```css
@media screen and (max-width: 640px) {
}
```

```css
@media screen and (min-width: 640px) {
}
```

```css
@media (min-width: 640px) {
}
```

```css
@media (min-width: 640px) and (max-width: 800px) {
}
```

---

[https://www.alsacreations.com/article/lire/930-css3-media-queries.html](https://www.alsacreations.com/article/lire/930-css3-media-queries.html)
