# Lab21-Capteurs-embarqu-s-Android
TP SENSOR – APPLICATION DE GESTION DES CAPTEURS ANDROID


Présentation

Ce projet est une application Android développée dans le cadre d’un travail pratique (TP) dont l’objectif est d’apprendre à manipuler les différents capteurs embarqués sur un smartphone. L’application permet de lister les capteurs disponibles, d’afficher leurs mesures en temps réel sous forme de graphiques, de calculer des grandeurs physiques (norme, orientation) et de réaliser des traitements simples comme la reconnaissance d’activité ou la boussole numérique.


Organisation du code source

Le projet est structuré en plusieurs packages :

- fragments : contient tous les écrans de l’application (un fragment par capteur ou groupe de capteurs).
- utils : contient les classes d’aide, notamment SensorFormatter pour la mise en forme des valeurs.
- views : contient les composants graphiques personnalisés, dont LineChartView pour le tracé des courbes en temps réel.


Étapes de réalisation (résumé technique)

Partie 1 – Préparation du projet
Configuration de l’environnement Android Studio, organisation des packages, création d’un menu latéral (Navigation Drawer) pour naviguer entre les capteurs.

Partie 2 – Affichage des capteurs disponibles
Utilisation de SensorManager pour lister tous les capteurs présents sur l’appareil. Pour chaque capteur, affichage des informations techniques : identifiant, fabricant, version, résolution, consommation électrique, etc.

Partie 3 – Création d’un graphe simple pour les mesures
Développement d’une vue personnalisée LineChartView capable de dessiner des courbes en temps réel sans utiliser de bibliothèque externe. Cette vue gère le traçage des valeurs successives sur un axe temps glissant.

Partie 4 – Température, humidité, proximité et champ magnétique
Implémentation d’un fragment générique SensorGraphFragment réutilisable. Gestion des valeurs simples (température, humidité, proximité) et calcul de la norme (magnitude) pour le champ magnétique. Un système de simulation permet de tester sur émulateur sans capteurs physiques.

Partie 5 – Accéléromètre, gravité et gyroscope
Mesure des mouvements sur les trois axes X, Y, Z. Affichage des trois courbes simultanément. Calcul de la norme (racine carrée de la somme des carrés) pour visualiser l’intensité globale du mouvement, utile pour détecter des chocs ou des secousses.

Partie 6 – Compteur de pas et économie d’énergie
Utilisation du capteur TYPE_STEP_COUNTER pour compter les pas depuis le dernier redémarrage. Gestion de la permission ACTIVITY_RECOGNITION (obligatoire sous Android 10 et supérieur). Optimisation de la batterie : libération des capteurs dans la méthode onPause() pour éviter une consommation inutile.

Partie 7 – Boussole numérique
Fusion des données de l’accéléromètre et du magnétomètre. Calcul de la matrice de rotation à l’aide de SensorManager.getRotationMatrix() puis de l’orientation (azimut) via SensorManager.getOrientation(). Affichage de l’angle par rapport au Nord géographique.

Partie 8 – Reconnaissance simple d’activité
Implémentation d’un filtre passe-bas (low-pass filter) pour isoler le mouvement réel de la gravité. Classification heuristique des états : Immobile (accélération proche de 0), Marche (oscillations régulières), Saut (pic d’accélération), Téléphone à plat (orientation et gravité fixes). Détection basée sur des seuils simples, sans apprentissage automatique.

Partie 9 – Intégration finale dans MainActivity
Centralisation de la navigation : chaque élément du menu latéral remplace le fragment courant dans le conteneur principal. Gestion du back stack pour permettre le retour en arrière cohérent.

Partie 10 – Tests et validation
Procédure de test pour chaque capteur (vérification des valeurs, des seuils, du graphique, des permissions). Validation sur appareil réel et sur émulateur (mode simulé).


Synthèse pédagogique

Ce TP illustre de manière progressive comment une application Android peut exploiter la richesse des capteurs embarqués. Les concepts abordés sont :

- la découverte et la configuration des capteurs via SensorManager ;
- l’acquisition périodique des données avec SensorEventListener ;
- la visualisation graphique temps réel sans librairie externe ;
- le calcul de grandeurs dérivées (norme, matrice de rotation, orientation) ;
- la fusion de capteurs (accéléromètre + magnétomètre) ;
- le traitement simple du signal (filtre passe-bas) ;
- la gestion des permissions sensibles et l’optimisation énergétique.

Dans un contexte industriel, cette approche peut être enrichie par l’utilisation de machine learning (TensorFlow Lite) pour une reconnaissance d’activité plus robuste, et par des services d’arrière-plan (Service ou WorkManager) pour une collecte continue.


Démonstration








L’application finale permet de :

- lister tous les capteurs du téléphone avec leurs caractéristiques ;
- visualiser en temps réel les courbes de l’accéléromètre, du gyroscope, du magnétomètre, de la température, de l’humidité et de la proximité ;
- afficher le nombre de pas et l’angle de la boussole ;
- reconnaître si l’utilisateur est immobile, en marche ou en train de sauter.

Un système de simulation intégré rend l’application pleinement fonctionnelle sur émulateur, même en l’absence de capteurs physiques.


Conclusion

Ce TP constitue une base solide pour toute application Android nécessitant l’utilisation de capteurs. Il met en œuvre des bonnes pratiques telles que la libération des ressources, la séparation des responsabilités (fragments, vues personnalisées, utilitaires) et la gestion des différences entre versions d’Android. Les compétences acquises peuvent être réutilisées dans des projets de santé connectée, de jeux mobiles, de réalité augmentée ou de monitoring industriel.
