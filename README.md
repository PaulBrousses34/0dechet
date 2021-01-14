# **Projet de fin de formation 0'déchet** 



![Logo 0'Déchet](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/logo.png)


-----------------------------------------------------------------------------------------------------------
## Les contributeurs ##

- Manon Furrer
- Laëtitia Georgelin
- Lucas Lefebvre
- Steven Renaux
- Paul Brousses

-----------------------------------------------------------------------------------------------------------

[Voir le site Web](https://0-dechet.net)

#### Site de recette écologique "Do It Yourself !"


-----------------------------------------------------------------------------------------------------------


## 1. Rôles

- Product Owner : Manon
- Scrum Master : Steven
- Git Master : Lucas
- Lead Dev Front : Laëtitia
- Lead Dev Back : Paul


## 2. Les objectifs du site


Le site Internet permettra de réunir toutes les recettes 0 déchet et écologiques  des utilisateurs, pour les produits d’entretien de la maison (lessive, produit pour  le sol etc...), d’hygiène et de beauté (shampoing, crème, déodorant etc...). 
La plupart de ces astuces étant actuellement généralement données  individuellement dans des blogs ou les sites persos, il est difficile de s’y retrouver  ou de savoir quoi choisir.


## 3. La cible

Personnes soucieuses de l’environnement, soucieuses de leur santé, et/ou de  leur portefeuille. 
Tout âge, « plutôt » jeune actifs et familles.


## 4. Spécificités techniques


### a. Accessibilité

L'application sera développé en Mobile First et sera disponible en 2 types d'affichage : Desktop et Mobile.

### b. Technologies utilisées

- Front : Twig, Bootstrap, Javascript Vanilla, jQuery
- Back : Symfony5, MySQL, Adminer
- Autres : Git, AWS, noip.com, Let's Encrypt


## 5. Fonctionnalités

### a. Permissions

L’application se comporte différemment selon le statut du visiteur.  Nous avons identifié trois types de visiteurs :  
- Anonyme : le visiteur anonyme 
- Utilisateur : le visiteur connecté 
- Administrateur : le visiteur connecté et disposant des droits d’administration  permettant d’accéder à la partie BackOffice 
Ces trois profils types d’utilisateurs ont le même point d’entrée sur  l’application, mais pas les mêmes possibilités. 

### b. Fonctionnalités en fonction des permissions

Un utilisateur anonyme peut : 
- naviguer sur le site Internet 
- rechercher des recettes 
- filtrer les recettes selon les types, sous catégories, catégories - trier les recettes selon la note ou la difficulté 
- s’inscrire ou se connecter sur le site Internet 

Un utilisateur connecté peut, en plus : 
- ajouter des recettes 
- ajouter des commentaires aux recettes 
- noter les recettes 

Un utilisateur Admin peut, en plus :  
- modérer les recettes et commentaires 
- accéder au BackOffice 



### c. Fonctionnalités supplémentaires possibles 

- Visualiser toutes les recettes d’un autre utilisateur 
- Gestion des favoris par les utilisateurs connectés 
- Possibilité de vidéo à la place de l’image 
- Ajout de tags 
- Afficher une partie blog/Newsletter sur le site (gérée par les Admin) - Ajout d’une table ingrédients permettant la recherche par ingrédient - Ajout du nombre de vues sur chaque recette 
- Abonnement à une newsletter pour les utilisateurs

## 6. Données

### a. MCD

![Modèle Conceptuel de Données](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/MCD.png)

WHO HAS FOR, 11 TYPE, 1N SUB_CATEGORY 
TYPE: name, slug 
HAVE, 0N RECIPE, 11 COMMENT: 
COMMENT: title, content, status 
WRITE, 0N USER, 11 COMMENT 
SUB_CATEGORY: name, slug 
CONCERNED, 11 RECIPE, 0N TYPE 
RECIPE: name, ingredient, equipment, content, duration, difficulty,  conservation, average_rate, image, slug, status 
WHO OWN, 0N USER, 01 RECIPE 
USER :email, username, password, roles, image, slug 
OWN, 1N CATEGORY, 11 SUB_CATEGORY 
CATEGORY: name, slug 
GET, 0N RECIPE, 11 RATE 
RATE: rate 
GIVE BY, 0N USER, 01 RATE

### b. Dico des données


|Table|Champ|Type|Spécificités|
|---    |:-:    |:-:    |:-:    |
|Category|id|INT|PRIMARY KEY, NOT NULL, AUTO_INCREMENT, UNSIGNED |
||name|VARCHAR (255)|NOT NULL|
||createdAt|TIMESTAMP|NOT NULL, CURRENT_TIMESTAMP|
||updatedAt|TIMESTAMP|NULL|
||slug|VARCHAR (255)|NOT NULL|
|SubCategory|id|INT|PRIMARY KEY, NOT NULL, AUTO_INCREMENT, UNSIGNED |
||name|VARCHAR (255)|NOT NULL|
||createdAt|TIMESTAMP|NOT NULL, CURRENT_TIMESTAMP|
||updatedAt|TIMESTAMP|NULL|
||slug|VARCHAR (255)|NOT NULL|
||category|ENTITY|NOT NULL|
|Type|id|INT|PRIMARY KEY, NOT NULL, AUTO_INCREMENT, UNSIGNED |
||name|VARCHAR (255)|NOT NULL|
||createdAt|TIMESTAMP|NOT NULL, CURRENT_TIMESTAMP|
||updatedAt|TIMESTAMP|NULL|
||slug|VARCHAR (255)|NOT NULL|
||Sous_categorie|ENTITY|NOT NULL|
|Rate|id|INT|PRIMARY KEY, NOT NULL, AUTO_INCREMENT, UNSIGNED |
||rate|INT|NOT NULL|
||createdAt|TIMESTAMP|NOT NULL, CURRENT_TIMESTAMP|
||updatedAt|TIMESTAMP|NULL|
||user|ENTITY|NULL|
||recipe|ENTITY|NOT NULL|
|Recipe|id|INT|PRIMARY KEY, NOT NULL, AUTO_INCREMENT, UNSIGNED |
||name|VARCHAR (255)|NOT NULL|
||ingredient|Array|NOT NULL|
||equipment|Array|NOT NULL|
||content|TEXT|NOT NULL|
||duration|INT|NOT NULL|
||difficulty|INT|NOT NULL|
||conservation|INT|NULL|
||image|VARCHAR (255)|NULL|
||status|BOOL|NOT NULL(Default 1)|
||average_rate|INT|NULL|
||slug|VARCHAR (255)|NOT NULL|
||type|ENTITY|NOT NULL|
||user|ENTITY|NULL|
||createdAt|TIMESTAMP|NOT NULL, CURRENT_TIMESTAMP|
||updatedAt|TIMESTAMP|NULL|
|Comment|id|INT|PRIMARY KEY, NOT NULL, AUTO_INCREMENT, UNSIGNED |
||title|VARCHAR (255)|NOT NULL|
||content|VARCHAR (50000)|NOT NULL|
||recipe|ENTITY|NOT NULL|
||user|ENTITY|NOT NULL|
||status|BOOL|NOT NULL(Default 1)|
||createdAt|TIMESTAMP|NOT NULL, CURRENT_TIMESTAMP|
||updatedAt|TIMESTAMP|NULL|
|User|id|INT|PRIMARY KEY, NOT NULL, AUTO_INCREMENT, UNSIGNED |
||email|VARCHAR (255)|NOT NULL|
||username|VARCHAR (255)|NOT NULL|
||password|VARCHAR (255)|NOT NULL|
||rôles|JSON|NOT NULL|
||image|VARCHAR (255)|NULL|
||slug|VARCHAR (255)|NOT NULL|
||createdAt|TIMESTAMP|NOT NULL, CURRENT_TIMESTAMP|
||updatedAt|TIMESTAMP|NULL|

## 7. Structure du site

### a. Arborescence

![Arborescence](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/arborescence.png)



















### e) User stories


|En tant que|Je veux pouvoir|Afin de|
|---    |:-:    |:-:    |
| Visiteur |Consulter les actualités|Me tenir informé de l’actualité|       
|       |Consulter l’agenda|Me tenir informé des événements à venir |
|       |Consulter les informations juridiques|Obtenir des renseignements d’ordre juridique|
|       |En savoir plus sur l’AMF34|Afin de connaître l’association et ses objectifs|
|       |Contacter un administrateur via un formulaire de contact|Obtenir de renseignements, proposer quelque chose ou porter une réclamation|
|       |Obtenir un devis et/ou souscrire à une assurance|Souscrire ou obtenir un devis |
|       |Rechercher un élément du site via un moteur de recherche|Accéder rapidement à une information précise|
| Utilisateur connecté |Accéder à l’annuaire des membres|Rechercher un numéro de téléphone, une adresse email, des informations sur un membre, ...|
| Administrateur |Ajouter, modifier, supprimer un article|Gérer le contenu du site |
|       |Ajouter, modifier, supprimer un membre|Gérer le contenu du site |
|       |Ajouter, modifier, supprimer un évènement|Gérer le contenu du site|

### f) Dictionnaire des routes

|Controller|URL|HTTP Method|Method|Title|Content|
|---    |:-:    |:-:    |:-:    |:-:    |--:    |
| **FrontOffice** |
|HomeController|/|GET|home|Accueil|Actu et agenda|
| |/contact|GET-POST|contact|Contact|Formulaire et infos|
|InfoController|/actualites|GET|Browse|Actualités|Liste de toutes les actualités|
| |/actualites/{slug}|GET|Read|Article {title}|Un article|
|EventController|/agenda|GET|Browse|Les événements|Liste des événements|
||/agenda/{slug}|GET|Read|Evenement {title}|Un evenement|
|UserController|/profil/{id}|GET|Read|Mon espace personnel|Affiche les informations utilisateurs et autres membres|
||/profil/edition/{id}|GET-POST|Edit|Modifier mon profil|Affiche le formulaire de modification du profil|
||/profil/suppression/{id}|DELETE|Delete|Bouton de suppression|Supprimer mon profil|
|SecurityController|/connexion|GET – POST|app_login|Connexion|Formulaire de connexion|
||/deconnexion|POST|app_logout|Déconnexion|Bouton ou lien de deconnexion|
| **BackOffice** |
|InfoCrudController|/admin/actualites|GET|Browse|Toutes les actualités|Liste des actualités|
||/admin/actualites/{id}|GET|Read|{title} de l'article|Affichage d’un article en particulier|
||/admin/actualites/edition/{id}|GET-POST|Edit|Modifier un article|Formulaire de modification de l’article|
||/admin/actualites/ajouter|GET-POST|Add|Ajouter un article|Formulaire d’ajout d’un article|
||/admin/actualites/suppression/{id}|DELETE|Delete|Suppression d'un article|Bouton de suppression d'un article|
|EventCrudController|/admin/evenement|GET|Browse|Liste de toutes les evenements|Affichage de la liste des evenements|
||/admin/evenement/{id}|GET|Read|Evenement {name}|Affichage d'un evenement|
||/admin/evenement/edition/{id}|GET-POST|Edit|Modifier un evenement|Formulaire de modification d'un evenement|
||/admin/evenement/ajouter|GET-POST|Add|Ajouter un evenement|Formulaire d’ajout d'un evenement|
||/admin/evenement/suppression/{id}|DELETE|Delete|Suppression d'un evenement|Bouton de suppression d'un evenement|
|UtilisateurCrudController|/admin/utilisateurs|GET|Browse|Liste de tous les utilisateurs|Affichage de la liste des utilisateurs|
||/admin/utilisateur/{id}|GET|Read|Utilisateur {name}|Affichage d'un utilisateur|
||/admin/utilisateur/edition/{slug}|GET-POST|Edit|Modifier un utilisateur|Formulaire de modification d'un utilisateur|
||/admin/utilisateur/ajouter|GET-POST|Add|Ajouter un utilisateur|Formulaire d’ajout d’un utilisateur|
||/admin/utilisateur/suppression/{id}|DELETE|Delete|Suppression d'un utilisateur|Bouton de suppression d'un utilisateur|




### h) Modèle Conceptuel de Données

Incomplet en attente de validation et de precisions supplémentaires 

![Modèle Conceptuel de Données](https://raw.githubusercontent.com/PaulBrousses34/AMF34/master/AMF34/public/images/MCD.png)


## 4. Organisation

### a) Planning

Le développement du site se fera sur 4 semaines. Suite à la mise en production une veille technologique est à prévoir. Le développement du site ne pourra commencer que lorsque le cahier des charges sera complet. Le travail s’effectuera selon les principes de la méthodes Agile Scrum les cycles de développement seront donc découpés en sprint d'une semaine chacun de la manière suivante : 

|Sprint|Tâches|
|---    |:-:    |
|1|Intégration HTML/CSS, création de la base de données, création de fixtures|
|2|Création des Controllers et des méthodes, création des formulaires, création des templates associés à toutes les méthodes|
|3|Mise en en place des diverses contraintes, gestion des rôles, création et configuration BackOffice|
|4|Recherche et correction de bugs, tests unitaires et fonctionnels, mise en production|

### b) Gestion du versionning


Chaque jour le développement se fera sur une nouvelle branche Git se nommant 12/12 par exemple si la date du jour est le 12 décembre. Cela permet de récupérer facilement la version voulue. Chaque jour les tâches effectuées seront notées dans un cahier de bord afin de récupérer plus facilement une partie du code en cas de problème. 

