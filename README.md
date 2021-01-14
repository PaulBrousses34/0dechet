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


### b. Wireframes


![maquette1](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette1.png)
![maquette2](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette2.png)
![maquette3](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette3.png)
![maquette4](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette4.png)
![maquette5](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette5.png)
![maquette6](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette6.png)
![maquette7](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette7.png)
![maquette8](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette8.png)
![maquette9](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette9.png)
![maquette10](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette10.png)
![maquette11](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette11.png)
![maquette12](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette12.png)
![maquette13](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquette13.png)



## 8. Dictionnaire des routes

### a. FrontOffice

|Controller|URL|HTTP Method|Method|Title|Content|
|---    |:-:    |:-:    |:-:    |:-:    |--:    |
|MainController|/|GET|home|Accueil|Accueil de 0'dechet|
||/contact|GET-POST|contact|Contact|Page contact|
|UserController|/profil/{slug}|GET|Read|Mon espace personnel|Affiche les informations utilisateurs et autres membres|
||/profil/edition/{slug}|GET-POST|Edit|Modifier mon profil|Affiche le formulaire de modification du profil|
||/inscription|GET-POST|Add|Créer un profil|Formulaire d'inscription|
||/profil/suppression/{slug}|DELETE|Delete|Bouton de suppression|Supprimer mon profil|
|SecurityController|/connexion|GET – POST|app_login|Connexion|Formulaire de connexion|
||/deconnexion|POST|app_logout|Déconnexion|Bouton ou lien de deconnexion|
|RecipeController|/recette|GET|Browse|Toutes les recettes|
||recette/{slug}|GET|Read|{name} de la recette|Affichage d'une recette|
||recette/edition/{slug}|GET-POST|Edit|Modifier une recette|Affichage du formulaire de modification|
||recette/ajout|GET-POST|Add|Ajouter une recette|Affichage du formulaire d'ajout|
||recette/suppression/{id}|DELETE|delete|-|Bouton de supression|
||recette/type/{slug}|GET|browseByType|{name} du type|Affichage des recettes selon un type|
||recette/sous-categorie/{slug}|GET|browseBySousCategory|{name} de la sous-categorie|Affichage des recettes selon une sous-categorie|
||recette/categorie/{slug}|GET|browseByCategory|{name} de la categorie|Affichage des recettes selon une categorie|


### b.BackOffice

|Controller|URL|HTTP Method|Method|Title|Content|
|---    |:-:    |:-:    |:-:    |:-:    |--:    |
|RecipeController|/admin/recipe|GET|Browse|Toutes les recettes|Affichage de toutes les recettes|
||/admin/recipe/{id}|GET|Read|Affichage d'une recette|Affichage d'une recette|
||/admin/recipe/edit/{id}|GET|Edit|Modifier une recette|Formulaire de modification d'une recette|
||/admin/recipe/add|GET|Add|Ajouter une recette|Formulaire d'ajout d'une recette|
||/admin/recipe/delete/{id}|GET|Delete|-|Bouton de suppression|
|TypeController|/admin/type|GET|Browse|Toutes les types|Affichage de toutes les types|
||/admin/type/{id}|GET|Read|{name} du type|Affichage d'un type|
||/admin/type/edit/{id}|GET|Edit|Modifier un type|Formulaire de modification d'un type|
||/admin/type/add|GET|Add|Ajouter un type|Formulaire d'ajout d'un type|
||/admin/type/delete/{id}|GET|Delete|-|Bouton de suppression|
|SubCategoryController|/admin/sub_category|GET|Browse|Toutes les sous catégories|Affichage de toutes les sous catégories|
||/admin/sub_category/{id}|GET|Read|{name} d'une sous catégorie|Affichage d'une sous catégorie|
||/admin/sub_category/edit/{id}|GET|Edit|Modifier une sous catégorie|Formulaire de modification d'une sous catégorie|
||/admin/sub_category/add|GET|Add|Ajouter une sous catégorie|Formulaire d'ajout d'une sous catégorie|
||/admin/sub_category/delete/{id}|GET|Delete|-|Bouton de suppression|
|CategoryController|/admin/category|GET|Browse|Toutes les catégories|Affichage de toutes les catégories|
||/admin/category/{id}|GET|Read|{name} d'une catégorie|Affichage d'une catégorie|
||/admin/category/edit/{id}|GET|Edit|Modifier une catégorie|Formulaire de modification d'une catégorie|
||/admin/category/add|GET|Add|Ajouter une catégorie|Formulaire d'ajout d'une catégorie|
||/admin/category/delete/{id}|GET|Delete|-|Bouton de suppression|
|CommentController|/admin/comment|GET|Browse|Tous les commentaires|Affichage de toutes les commentaires|
||/admin/comment/{id}|GET|Read|{title} d'un commentaire|Affichage d'un commentaire|
||/admin/comment/edit/{id}|GET|Edit|Modifier un commentaire|Formulaire de modification d'un commentaire|
||/admin/comment/add|GET|Add|Ajouter un commentaire|Formulaire d'ajout d'un commentaire|
||/admin/comment/delete/{id}|GET|Delete|-|Bouton de suppression|
|UserController|/admin/user|GET|Browse|Tous les utilisateurs|Affichage de toutes les utilisateurs|
||/admin/user/{id}|GET|Read|{username}|Affichage d'un utilisateur|
||/admin/user/edit/{id}|GET|Edit|Modifier un utilisateur|Formulaire de modification d'un utilisateur|
||/admin/user/add|GET|Add|Ajouter un utilisateur|Formulaire d'ajout d'un utilisateur|
||/admin/user/delete/{id}|GET|Delete|-|Bouton de suppression|


## 9. User stories


|En tant que|Je veux pouvoir|Afin de|
|---    |:-:    |:-:    |
| Visiteur |visualiser toutes les recettes|avoir une vision d'ensemble sur les recettes du site|       
|       |trier les recettes par note|visualiser facilement les meilleures recettes|
|       |trier les recettes par difficulté|visualiser facilement les recettes adaptées à mon niveau|
|       |filtrer les recettes par catégories|pouvoir accéder plus facilement aux recettes que je recherche|
|       |filtrer les recettes par sous-catégories|pouvoir accéder plus facilement aux recettes que je recherche|
|       |filtrer les recettes par types|pouvoir accéder plus facilement aux recettes que je recherche|
|       |afficher toutes les recettes d'un utilisateur|visualiser toutes les recettes qu'il a posté|
|       |rechercher une recette|trouver une recette correspondant à mon besoin|
|       |m'inscrire sur le site|pouvoir accéder à de nouvelles fonctionnalités|
| Utilisateur connecté |se connecter|pouvoir accéder à plus de fonctionnalités sur le site|
|       |ajouter une recette|partager mes recettes avec la communnauté du site|
|       |ajouter une recette en favoris|retrouver mes recettes préférées directement sur mon profil|
|       |noter une recette|pouvoir donner mon avis|
|       |commenter une recette|pouvoir donner mon avis|
|       |modifier mon profil|modifier mon mot de passe ou mon adresse email|
|       |supprimer mon profil|me désinscrire du site|
|       |associer une vidéo à ma recette|montrer étape par étape la réalisation de la recette|
| Administrateur |Ajouter, modifier, supprimer des recettes|Gérer le contenu du site |
|       |Ajouter, modifier, supprimer des utilisateurs|Gérer le contenu du site |
|       |Ajouter, modifier, supprimer des commentaires|Gérer le contenu du site|
|       |Ajouter, modifier, supprimer des catégories|Gérer le contenu du site |
|       |Ajouter, modifier, supprimer des sous-catégories|Gérer le contenu du site|
|       |Ajouter, modifier, supprimer des types|Gérer le contenu du site|



## 10. Charte Graphique

### a. Couleurs


![Palette couleur](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/paletteCouleur.png)


### b. Maquette avec couleur

![Maquette couleur 1](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquetteCouleur1.png)
![Maquette couleur 2](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/maquetteCouleur2.png)

### c. Logo

![Propositions logos](https://raw.githubusercontent.com/PaulBrousses34/0dechet/master/public/assets/images/propLogo.png)

