# Bienvenue sur la documentation de l'API Business Cloud Mobile

Vous trouverez ici, l'ensemble de la documentation relative à l'API.

## Intallation de l'API en local

* `Récupération du projet` - [Lien du GitHub](https://github.com/Sebastien-Lechat/Business-Cloud-Mobile-API).
* `Exécution de commande` - Ensemble des commandes nécessaire à exécuter pour le lancement du projet.

```
npm install
npm start
```
* `Lancement du serveur` - Le serveur est lancé à l'adresse suivante : [http://localhost:3000/](http://localhost:3000/)

## Ensemble des module nécessaires

* `Express` - [Lien du module](https://www.npmjs.com/package/express).
* `Body-parser` - [Lien du module](https://www.npmjs.com/package/express).
* `Bcrypt` - [Lien du module](https://www.npmjs.com/package/bcrypt).
* `Mongoose` - [Lien du module](https://www.npmjs.com/package/mongoose).
* `JsonWebToken` - [Lien du module](https://www.npmjs.com/package/jsonwebtoken).
* `Nodemailer` - [Lien du module](https://www.npmjs.com/package/nodemailer).
* `Cors` - [Lien du module](https://www.npmjs.com/package/cors).
* `Socket.io` - [Lien du module](https://www.npmjs.com/package/socket.io).
* `Firebase cloud messaging` - [Lien de la documentation](https://firebase.google.com/docs).

## Documentation des routes

### Authentification
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Connexion

---

**Route de connexion pour n'importe quel type d'utilisateur.**

**URL** : `/auth/login`

**Methode** : `POST`

**Token requis** : `NON`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| email | string | Email de l'utilisateur | ✔️ |
| password | string | Mot de passe de l'utilisateur | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message" : "Successfully connected",
    "user" : {
        "id":"",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "type" : "",
        "address" : "",
        "zip" : "",
        "city" : "",
        "currency" : "",
        "country" : "",
        "token" : "",
        "refreshToken" : "",
        "createdAt" : "",
        "updatedAt" : "",
        "userId": "",
        "isActive": "",
    }
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "101001",
    "message": "Email/Password is missing"
}
```

**Condition** : Mauvais mot de passe.

**Code** : `400`

```json
{
    "error": true,
    "code": "101002",
    "message": "Invalid password"
}
```

---

#### Inscription

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
**Route de d'inscription d'un utilisateur (client ou entreprise).**

**URL** : `/auth/register`

**Methode** : `POST`

**Token requis** : `NON`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| name | string | Nom et prénom de l'utilisateur ou de l'entreprise | ✔️ | 
| email | string | Email de l'utilisateur ou de l'entreprise | ✔️ | 
| phone | string | Téléphone de l'utilisateur ou de l'entreprise | - |
| birthdayDate | date | Date de naisse de l'utilisateur | - |
| password | string | Mot de passe de l'utilisateur ou de l'entreprise | ✔️ | 
| address | string | Adresse de l'utilisateur ou de l'entreprise | - |
| zip | string | Code postal de l'utilisateur ou de l'entreprise | - |
| city | string | Ville de l'utilisateur ou de l'entreprise | - |
| country | string | Pays | - |
| numTVA | string | Numéro de TVA de l'entreprise | - |
| numSIRET | string | Numéro de SIRET de l'entreprise | - |
| numRCS | string | Numéro de RCS de l'entreprise | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successfully registred"
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "101051",
    "message": "Missing important fields"
}
```

**Condition** : Adresse email invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "101052",
    "message": "Invalid email addresse"
}
```

**Condition** : Numéro de téléphone invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "101053",
    "message": "Invalid phone number"
}
```

**Condition** : Mot de passe invalide ou à faible sécurité (Une majuscule, un numéro, un caractère spécial, et de 7 à 30 charactères).

**Code** : `400`

```json
{
    "error": true,
    "code": "101054",
    "message": "Invalid password format"
}
```

**Condition** : Numéro de TVA invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "101055",
    "message": "Invalid TVA number"
}
```

**Condition** : Numéro de SIRET invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "101056",
    "message": "Invalid SIRET number"
}
```

**Condition** : Numéro de RCS invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "101057",
    "message": "Invalid RCS number"
}
```

**Condition** : Date de naisseance invalide (DD-MM-YYY).

**Code** : `400`

```json
{
    "error": true,
    "code": "101058",
    "message": "Invalid date format"
}
```

**Condition** : L'email est déjà utilisé par un autre utilisateur.

**Code** : `400`

```json
{
    "error": true,
    "code": "101059",
    "message": "This email is already used"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Mot de passe oublié

---

**Route de récupération du mot depasse utilisateur. Le mail contient un lien de redirection sur le site pour modifier le mot de passe.**

**URL** : `/auth/password-lost`

**Methode** : `POST`

**Token requis** : `NON`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| email | string | Email de l'utilisateur | xxxx |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Email successfully send"
}
```

##### Requête échouée

**Condition** : Echec de l'envoi du mail.

**Code** : `500`

```json
{
    "error": true,
    "code": "101101",
    "message": "Internal server error, email can not be send"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Vérification de l'email (envoi)

---

**Route d'envoi d'un email contenant un code de vérification à un utilisateur après son inscription, ou si il change de mail dans son profil.**

**URL** : `/auth/request-verify-email`

**Methode** : `POST`

**Token requis** : `NON`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| email | string | Email de l'utilisateur | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Email successfully send"
}
```

##### Requête échouée

**Condition** : Echec de l'envoi du mail.

**Code** : `500`

```json
{
    "error": true,
    "code": "500001",
    "message": "Internal server error, email can not be send"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Vérification de l'email (vérification)

---

**Route de vérification de l'email grâce au code reçu dans le mail de la requête précédente. Le code est valable 10 minutes.**

**URL** : `/auth/verify-email`

**Methode** : `POST`

**Token requis** : `NON`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| email | string | Email de l'utilisateur | ✔️ | 
| code | string | Code à 6 chiffre reçu dans le mail | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful verification"
}
```

##### Requête échouée

**Condition** : Mauvais code.

**Code** : `400`

```json
{
    "error": true,
    "code": "101201",
    "message": "Wrong code"
}
```

##### Requête échouée

**Condition** : Code expiré.

**Code** : `400`

```json
{
    "error": true,
    "code": "101202",
    "message": "This code is no longer valid"
}
```

---

### Profil utilisateur
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Récupération du profil

---

**Route de récupération des informations de son profil utilisateur.**

**URL** : `/account`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| - | - | - | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful profil acquisition",
    "user" : {
        "id":"",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "type" : "",
        "address" : "",
        "zip" : "",
        "city" : "",
        "currency" : "",
        "country" : "",
        "activity" : "",
        "numTVA" : "",
        "numSIRET" : "",
        "numRCS" : "",
        "token" : "",
        "refreshToken" : "",
        "createdAt" : "",
        "updatedAt" : "",
        "userId": "",
        "isActive": "",
        "verify_email": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```
---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modification des informations personnelles

---

**Route de modification des informations personnelles, des informations de contact et deavatar de l'utilisateur.**

**URL** : `/account/information`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| avatar | file | Avatar de l'utilisateur | - | 
| name | string | Nom et prénom de l'utilisateur ou de l'entreprise | - | 
| email | string | Email de l'utilisateur ou de l'entreprise | - | 
| phone | string | Téléphone de l'utilisateur ou de l'entreprise | - |
| birthdayDate | date | Date de naisse de l'utilisateur | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Profile successfully updated",
    "user" : {
        "id":"",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "type" : "",
        "address" : "",
        "zip" : "",
        "city" : "",
        "currency" : "",
        "country" : "",
        "activity" : "",
        "numTVA" : "",
        "numSIRET" : "",
        "numRCS" : "",
        "token" : "",
        "refreshToken" : "",
        "createdAt" : "",
        "updatedAt" : "",
        "userId": "",
        "isActive": "",
        "verify_email": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

**Condition** : Adresse email invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "102051",
    "message": "Invalid email addresse"
}
```

**Condition** : Numéro de téléphone invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "102052",
    "message": "Invalid phone number"
}
```

**Condition** : Erreur lors de l'enregistrement de l'avatar.

**Code** : `500`

```json
{
    "error": true,
    "code": "500002",
    "message": "Internal server error, avatar can not be saved"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modification du mot de passe

---

**Route de modification du mot de passe de l'utilisateur.**

**URL** : `/account/password`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| email | string | Email de l'utilisateur | ✔️ | 
| oldPassword | string | Ancien mot de passe de l'utilisateur | ✔️ | 
| newPassword | string | Nouveau mot de passe de l'utilisateur | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Password successfully updated",
    "user" : {
        "id":"",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "type" : "",
        "address" : "",
        "zip" : "",
        "city" : "",
        "currency" : "",
        "country" : "",
        "activity" : "",
        "numTVA" : "",
        "numSIRET" : "",
        "numRCS" : "",
        "token" : "",
        "refreshToken" : "",
        "createdAt" : "",
        "updatedAt" : "",
        "userId": "",
        "isActive": "",
        "verify_email": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

**Condition** : Ancien mot de passe invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "102101",
    "message": "Invalid old password"
}
```

**Condition** : Nouveau mot de passe invalide ou à faible sécurité.

**Code** : `400`

```json
{
    "error": true,
    "code": "102102",
    "message": "Invalid new password"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modification de l'adresse

---

**Route de modification des information de location de l'utilisateur.**

**URL** : `account/address`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| address | string | Adresse de l'utilisateur ou de l'entreprise | - |
| zip | string | Code postal de l'utilisateur ou de l'entreprise | - |
| city | string | Ville de l'utilisateur ou de l'entreprise | - |
| country | string | Pays | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Address successfully updated",
    "user" : {
        "id":"",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "type" : "",
        "address" : "",
        "zip" : "",
        "city" : "",
        "currency" : "",
        "country" : "",
        "activity" : "",
        "numTVA" : "",
        "numSIRET" : "",
        "numRCS" : "",
        "token" : "",
        "refreshToken" : "",
        "createdAt" : "",
        "updatedAt" : "",
        "userId": "",
        "isActive": "",
        "verify_email": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

**Condition** : Code postal invalid.

**Code** : `400`

```json
{
    "error": true,
    "code": "102151",
    "message": "Invalid zip code"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modification des informations entreprise

---

**Route de modification des informations liées à l'entreprise d'un utilisateur.**

**URL** : `/account/enterprise`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| numTVA | string | Numéro de TVA de l'entreprise | - |
| numSIRET | string | Numéro de SIRET de l'entreprise | - |
| numRCS | string | Numéro de RCS de l'entreprise | - |
| currency | string | Monnaie avec laquelle les factures seront générées pour le client | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Enterprise successfully updated",
    "user" : {
        "id":"",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "type" : "",
        "address" : "",
        "zip" : "",
        "city" : "",
        "currency" : "",
        "country" : "",
        "activity" : "",
        "numTVA" : "",
        "numSIRET" : "",
        "numRCS" : "",
        "token" : "",
        "refreshToken" : "",
        "createdAt" : "",
        "updatedAt" : "",
        "userId": "",
        "isActive": "",
        "verify_email": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

**Condition** : Numéro de TVA invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "102201",
    "message": "Invalid TVA number"
}
```

**Condition** : Numéro de SIRET invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "102202",
    "message": "Invalid SIRET number"
}
```

**Condition** : Numéro de RCS invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "102203",
    "message": "Invalid RCS number"
}
```
---

### Utilisateurs
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Liste des utilisateurs

---

**Route d'obtention de la liste des utilisateurs en fonction des permissions. Un client verra son employé référent et le gérant, un employé verra ses clients et les autres employés, et pour finir le gérant verra l'ensemble des utilisateurs de l'application.**

**URL** : `/users`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| - | - | - | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful users acquisition",
    "users": [{
        "id": "",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "createdAt" : "",
        "updatedAt" : "",
        "userId": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Récupération d'un utilisateur

---

**Route de récupération des informations d'un utilisateur grâce à son id.**

**URL** : `/user/:id`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de l'utilisateur cible | ✔️ | 


##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful user acquisition",
    "user": {
        "id":"",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "type" : "",
        "address" : "",
        "zip" : "",
        "city" : "",
        "currency" : "",
        "country" : "",
        "activity" : "",
        "numTVA" : "",
        "numSIRET" : "",
        "numRCS" : "",
        "createdAt" : "",
        "updatedAt" : "",
        "userId": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Créer un client

---

**Route de création d'un client par un employé ou un gérant.**

**URL** : `/customer`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| userId | string | ID de l'employé référent du client | - | 
| name | string | Nom et prénom de l'utilisateur ou de l'entreprise | ✔️ | 
| email | string | Email de l'utilisateur ou de l'entreprise | ✔️ | 
| phone | string | Téléphone de l'utilisateur ou de l'entreprise | - |
| address | string | Adresse de l'utilisateur ou de l'entreprise | - |
| zip | string | Code postal de l'utilisateur ou de l'entreprise | - |
| city | string | Ville de l'utilisateur ou de l'entreprise | - |
| country | string | Pays | - |
| numTVA | string | Numéro de TVA de l'entreprise | - |
| numSIRET | string | Numéro de SIRET de l'entreprise | - |
| numRCS | string | Numéro de RCS de l'entreprise | - |
| currency | string | Monnaie avec laquelle les factures seront générée pour le client | - |
| note | string | Annotation sur le client sur le client | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Customer successfully created",
    "customer": {
        "id":"",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "type" : "",
        "address" : "",
        "zip" : "",
        "city" : "",
        "currency" : "",
        "country" : "",
        "activity" : "",
        "numTVA" : "",
        "numSIRET" : "",
        "numRCS" : "",
        "createdAt" : "",
        "updatedAt" : "",
        "userId": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "103151",
    "message": "Missing important fields"
}
```

**Condition** : Adresse email invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103152",
    "message": "Invalid email addresse"
}
```

**Condition** : Numéro de téléphone invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103152",
    "message": "Invalid phone number"
}
```

**Condition** : Numéro de TVA invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103154",
    "message": "Invalid TVA number"
}
```

**Condition** : Numéro de SIRET invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103155",
    "message": "Invalid SIRET number"
}
```

**Condition** : Numéro de RCS invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103156",
    "message": "Invalid RCS number"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modifier un client

---

**Route de modification d'un client par un employé ou un gérant.**

**URL** : `/customer`

**Methode** : `PUT`

**Token requis** : ``

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| id | string | ID du client dont on veut modifier les informations | ✔️ |
| userId | string | ID de l'employé référent du client | - | 
| name | string | Nom et prénom de l'utilisateur ou de l'entreprise | - | 
| email | string | Email de l'utilisateur ou de l'entreprise | - | 
| phone | string | Téléphone de l'utilisateur ou de l'entreprise | - |
| address | string | Adresse de l'utilisateur ou de l'entreprise | - |
| zip | string | Code postal de l'utilisateur ou de l'entreprise | - |
| city | string | Ville de l'utilisateur ou de l'entreprise | - |
| country | string | Pays | - |
| numTVA | string | Numéro de TVA de l'entreprise | - |
| numSIRET | string | Numéro de SIRET de l'entreprise | - |
| numRCS | string | Numéro de RCS de l'entreprise | - |
| currency | string | Monnaie avec laquelle les factures seront générées pour le client | - |
| note | string | Annotation sur le client sur le client | - |


##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Customer successfully updated",
    "user": {
        "id":"",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "type" : "",
        "address" : "",
        "zip" : "",
        "city" : "",
        "currency" : "",
        "country" : "",
        "activity" : "",
        "numTVA" : "",
        "numSIRET" : "",
        "numRCS" : "",
        "createdAt" : "",
        "updatedAt" : "",
        "userId": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

**Condition** : Adresse email invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103201",
    "message": "Invalid email addresse"
}
```

**Condition** : Numéro de téléphone invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103202",
    "message": "Invalid phone number"
}
```

**Condition** : Numéro de TVA invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103203",
    "message": "Invalid TVA number"
}
```

**Condition** : Numéro de SIRET invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103204",
    "message": "Invalid SIRET number"
}
```

**Condition** : Numéro de RCS invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103205",
    "message": "Invalid RCS number"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer un client

---

**Route de suppression d'un client par un employé ou un gérant. La requête ne supprimera pas réellement l'utilisateur, elle le désactivera seulement.**

**URL** : `/customer/:id/:email`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID du client à supprimer | ✔️ | 
| :email | string | Email du client à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Customer successfully deleted"
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Créer un employé

---

**Route de création d'un employé par un gérant.**

**URL** : `/employee`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| idManager | string | ID du gérant | ✔️ |
| name | string | Nom et prénom de l'utilisateur ou de l'entreprise | ✔️ | 
| email | string | Email de l'utilisateur ou de l'entreprise | ✔️ | 
| phone | string | Téléphone de l'utilisateur ou de l'entreprise | ✔️ |
| password | string | Mot de passe de l'utilisateur ou de l'entreprise | ✔️ | 
| role | string | Rôle de l'employé au sein de l'entreprise | ✔️ |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Employee successfully created",
    "customer": {
        "idManager": "",
        "id":"",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "role" : "",
        "createdAt" : "",
        "updatedAt" : "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "103301",
    "message": "Missing important fields"
}
```

**Condition** : Adresse email invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103302",
    "message": "Invalid email addresse"
}
```

**Condition** : Numéro de téléphone invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103303",
    "message": "Invalid phone number"
}
```

**Condition** : Mot de passe invalide ou à faible sécurité.

**Code** : `400`

```json
{
    "error": true,
    "code": "103304",
    "message": "Invalid password"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modifier un employé

---

**Route de création d'un employé par un gérant.**

**URL** : `/employee`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| id | string | ID de l'employé à modifier | ✔️ | 
| name | string | Nom et prénom de l'utilisateur ou de l'entreprise | - | 
| email | string | Email de l'utilisateur ou de l'entreprise | - | 
| phone | string | Téléphone de l'utilisateur ou de l'entreprise | - |
| role | string | Rôle de l'employé au sein de l'entreprise | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Employee successfully updated",
    "customer": {
        "idManager": "",
        "id":"",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "role" : "",
        "createdAt" : "",
        "updatedAt" : "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```
**Code** : `400`

```json
{
    "error": true,
    "code": "103351",
    "message": "Missing important fields"
}
```

**Condition** : Adresse email invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103352",
    "message": "Invalid email addresse"
}
```

**Condition** : Numéro de téléphone invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103353",
    "message": "Invalid phone number"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer un employé

---

**Route de suppression d'un employé par un gérant. La requête ne supprimera pas réellement l'employé, elle le désactivera seulement.**

**URL** : `/employee/:id/:email`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de l'employé à supprimer | ✔️ | 
| :email | string | Email de l'employé à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Employee successfully deleted"
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

### Factures
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Liste des factures

---

**Route de récupération de la liste de ses factures pour un client, des factures de tout ses clients pour un employé et de tous les utilisateurs pour un gérant**

**URL** : `/bills`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| - | - | - | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful bills acquisition",
    "bills": [{
        "id": "",
        "status": "",
        "clientId": "",
        "entrepriseId": "",
        "billNum": "",
        "articles": [{
            "articleId": "",
            "quantity": "",
        },{...}],
        "currency": "",
        "totalHT": "",
        "totalTTC": "",
        "amountPaid": "",
        "deadline": "",
        "createdAt": "",
        "updatedAt": "",
        "payementDate": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Récupération d'une facture

---

**Route de récupération d'une facture. Un client ne peut récupérer que ses factures, un employé les factures de ses clients, et un gérant les factures de tous les utilisateurs.**

**URL** : `/bill/:id`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de la facture à récupérer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful bill acquisition",
    "bill": {
        "id": "",
        "status": "",
        "clientId": "",
        "entrepriseId": "",
        "billNum": "",
        "articles": [{
            "articleId": "",
            "quantity": "",
        },{...}],
        "currency": "",
        "taxe": "",
        "totalHT": "",
        "totalTTC": "",
        "amountPaid": "",
        "deadline": "",
        "createdAt": "",
        "updatedAt": "",
        "payementDate": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Créer une facture

---

**Route de création d'une facture pour les employés et les gérants.**

**URL** : `/bill`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| status | string | Statut de la facture | ✔️ | 
| clientId | string | ID du client lié à la facture | ✔️ | 
| entrepriseId | string | ID de l'entreprise du gérant | ✔️ | 
| billNum | string | Numéro unique de facture | ✔️ | 
| currency | string | Monnaie avec laquelle la facture sera généré | ✔️ |
| deadline | date | Date limite à laquelle le client peut payer la facture | ✔️ |
| taxe | string | Taxe appliquer sur la facture de manière globale | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Bill successfuly created",
    "bill": {
        "id": "",
        "status": "",
        "clientId": "",
        "entrepriseId": "",
        "billNum": "",
        "articles": [],
        "currency": "",
        "taxe": "",
        "totalHT": "",
        "totalTTC": "",
        "deadline": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

**Condition** : Numéro de facture invalide

**Code** : `400`

```json
{
    "error": true,
    "code": "104151",
    "message": "Invalid bill number"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modifier une facture

---

**Route de modification d'une facture par un employé ou un gérant.**

**URL** : `/bill`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| id | string | ID de la facture à modifier | ✔️ | 
| status | string | Statut de la facture | - | 
| clientId | string | ID du client lié à la facture | - | 
| billNum | string | Numéro unique de facture | - | 
| articles | array | Tableaux de l'ensemble des articles de la facture | - | 
| currency | string | Monnaie avec laquelle la facture sera généré | - |
| deadline | date | Date limite à laquelle le client peut payer la facture | - |
| taxe | string | Taxe appliquer sur la facture de manière globale | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Bill successfully updated",
    "bill": {
        "id": "",
        "status": "",
        "clientId": "",
        "entrepriseId": "",
        "billNum": "",
        "articles": [{
            "articleId": "",
            "quantity": "",
        },{...}],
        "currency": "",
        "taxe": "",
        "totalHT": "",
        "totalTTC": "",
        "amountPaid": "",
        "deadline": "",
        "createdAt": "",
        "updatedAt": "",
        "payementDate": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

**Condition** : Numéro de facture invalide

**Code** : `400`

```json
{
    "error": true,
    "code": "104201",
    "message": "Invalid bill number"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer une facture

---

**Route de suppression d'une facture par un employé ou un gérant.**

**URL** : `/bill/:id`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de la à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Bill successfully deleted"
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

### Devis
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Liste des devis

---

**Route de récupération de la liste de ses devis pour un client, des devis de tout ses clients pour un employé et de tous les utilisateurs pour un gérant.**

**URL** : `/estimates`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| - | - | - | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful etimates acquisition",
    "estimates": [{
        "id": "",
        "status": "",
        "clientId": "",
        "entrepriseId": "",
        "estimateNum": "",
        "articles": [{
            "articleId": "",
            "quantity": "",
        },{...}],
        "currency": "",
        "taxe": "",
        "totalHT": "",
        "totalTTC": "",
        "deadline": "",
        "createdAt": "",
        "updatedAt": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Récupération d'un devis

---

**Route de récupération d'un devis. Un client ne peut récupérer que ses devis, un employé les devis de ses clients, et un gérant les devis de tous les utilisateurs.**

**URL** : `/estimate/:id`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID du devis à récupérer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful bill acquisition",
    "estimate": {
        "id": "",
        "status": "",
        "clientId": "",
        "entrepriseId": "",
        "estimateNum": "",
        "articles": [{
            "articleId": "",
            "quantity": "",
        },{...}],
        "currency": "",
        "taxe": "",
        "totalHT": "",
        "totalTTC": "",
        "deadline": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Créer un devis

---

**Route de création d'un devis pour les employés et les gérants.**

**URL** : `/estimate`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| status | string | Statut du devis | ✔️ | 
| clientId | string | ID du client lié au devis | ✔️ | 
| entrepriseId | string | ID de l'entreprise du gérant | ✔️ | 
| estimateNum | string | Numéro unique de devis | ✔️ | 
| currency | string | Monnaie avec laquelle le devis sera généré | ✔️ |
| deadline | date | Date limite à laquelle le client peut accepter le devis | ✔️ |
| taxe | string | Taxe appliquer sur le devis de manière globale | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "estimate successfuly created",
    "estimate": {
        "id": "",
        "status": "",
        "clientId": "",
        "entrepriseId": "",
        "estimateNum": "",
        "articles": [],
        "currency": "",
        "taxe": "",
        "totalHT": "",
        "totalTTC": "",
        "deadline": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

**Condition** : Numéro de devis invalide

**Code** : `400`

```json
{
    "error": true,
    "code": "105151",
    "message": "Invalid estimate number"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modifier un devis

---

**Route de modification d'un devis par un employé ou un gérant.**

**URL** : `/estimate`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| id | string | ID du devis à modifier | ✔️ | 
| status | string | Statut du devis | - | 
| clientId | string | ID du client lié au devis | - | 
| estimateNum | string | Numéro unique de devis | - | 
| articles | array | Tableaux de l'ensemble des articles du devis | - | 
| currency | string | Monnaie avec laquelle le devis sera généré | - |
| deadline | date | Date limite à laquelle le client peut payer le devis | - |
| taxe | string | Taxe appliquer sur le devis de manière globale | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Estimate successfully updated",
    "estimate": {
        "id": "",
        "status": "",
        "clientId": "",
        "entrepriseId": "",
        "billNum": "",
        "articles": [{
            "articleId": "",
            "quantity": "",
        },{...}],
        "currency": "",
        "taxe": "",
        "totalHT": "",
        "totalTTC": "",
        "amountPaid": "",
        "deadline": "",
        "createdAt": "",
        "updatedAt": "",
        "payementDate": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

**Condition** : Numéro de devis invalide

**Code** : `400`

```json
{
    "error": true,
    "code": "104201",
    "message": "Invalid estimate number"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer un devis

---

**Route de suppression d'un devis par un employé ou un gérant.**

**URL** : `/estimate/:id`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID du devis à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Estimate successfully deleted"
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

### Articles
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Liste des articles

---

**Route de récupération de la liste des articles pour un gérant ou un employé.**

**URL** : `/articles`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| - | - | - | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful articles acquisition",
    "articles": [{
        "id": "",
        "name": "",
        "tva": "",
        "price": "",
        "accountNumber": "",
        "description": "",
        "createdAt": "",
        "updatedAt": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Créer un article

---

**Route de création d'un article pour un employé ou un gérant.**

**URL** : `/article`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| name | string | Nom de l'article | ✔️ | 
| accountNumber | number | Numéro de compte comptable de l'article | ✔️ | 
| price | number | Prix unitaire de l'article | ✔️ | 
| tva | number | TVA appliqué à l'article | ✔️ | 
| description | string | Description de l'article | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Article successfully created",
    "article": {
        "id": "",
        "name": "",
        "tva": "",
        "price": "",
        "accountNumber": "",
        "description": "",
        "createdAt": "",
        "updatedAt": "",
    } 

}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer un article

---

**Route de suppression d'un article par un employé ou un gérant.**

**URL** : `/article/:id`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de l'article à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Article successfully deleted"
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

### Notes de frais
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Liste des notes de frais

---

**Route de récupération de la liste des notes de frais pour un gérant ou un employé.**

**URL** : `/expense-employee`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| - | - | - | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful expenses acquisition",
    "expenses": [{
        "userExpenseNum": "",
        "id": "",
        "price": "",
        "accountNumber": "",
        "file": "",
        "description": "",
        "userId/idManager": "",
        "createdAt": "",
        "updatedAt": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

#### Créer une note de frais

---

**Route de création d'une note de frais pour les employés et les gérants.**

**URL** : `/expense-employee`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| userExpenseNum | string | Numéro unique de dépense | ✔️ | 
| userId/idManager | string | ID de l'employé ou du gérant créant la note de frais | ✔️ | 
| price | number | Montant de la note de frais  | ✔️ | 
| category | string | Category de la note de frais | ✔️ | 
| accountNumber | number | Numéro de compte comptable de la note de frais | ✔️ | 
| file | file | Document de justification de la note de frais | - | 
| description | string | Description de la note de frais | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Expense successfully created", 
    "expense": {
        "userExpenseNum": "",
        "id": "",
        "price": "",
        "accountNumber": "",
        "category": "",
        "file": "",
        "description": "",
        "userId/idManager": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer une note de frais

---

**Route de suppression d'une note de frais par un employé ou un gérant.**

**URL** : `/expense-employee/:id`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de la note de frais à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Expense employee successfully deleted"
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
### Projets

#### Liste des projets

---

**Route de récupération de la liste des projets pour un employé ou un gérant.**

**URL** : `/project`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| - | - | - | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful projects acquisition",
    "projects": [{
        "projectNum": "",
        "id": "",
        "title": "",
        "status": "",
        "clientId": "",
        "progression": "",
        "startDate": "",
        "deadline": "",
        "employees":  [""],
        "fixedRate": "",
        "hourlyRate": "",
        "estimateHour": "",
    },{...}]
}

```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Créer un projet

---

**Route de création d'un projet par un employé ou un gérant.**

**URL** : `/project`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| projectNum | string | Numéro unique de projet | ✔️ |
| title | string | Titre du projet | ✔️ | 
| status | string | Statut d'avancement du projet | ✔️ | 
| clientId | string | ID du client lié au projet | ✔️ | 
| progression | number | Progression du projet | - | 
| startDate | date | Date de début du projet | - | 
| deadline | date | Date d'échéance du projet | ✔️ | 
| employees | string | Liste des employés liés au projet | ✔️ | 
| fixedRate | date | Taux fixe | - | 
| hourlyRate | date | Taux horaire | - | 
| estimateHour | number | Nombre d'heure estimé du projet | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Project successfully created",
    "project": {
        "projectNum": "",
        "id": "",
        "title": "",
        "status": "",
        "clientId": "",
        "progression": "",
        "startDate": "",
        "deadline": "",
        "employees":  [""],
        "fixedRate": "",
        "hourlyRate": "",
        "estimateHour": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modifier un projet

---

**Route de modification d'un projet par un employé ou un gérant.**

**URL** : `/project`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| id | string | ID du projet à modifier | ✔️ |
| projectNum | string | Numéro unique de projet | - |
| title | string | Titre du projet | - | 
| status | string | Statut d'avancement du projet | - | 
| clientId | string | ID du client lié au projet | - | 
| progression | number | Progression du projet | - | 
| startDate | date | Date de début du projet | - | 
| deadline | date | Date d'échéance du projet | - | 
| employees | array | Liste des employés liés au projet | - | 
| fixedRate | date | Taux fixe | - | 
| hourlyRate | date | Taux horaire | - | 
| estimateHour | number | Nombre d'heures estimées à la réalisation du projet | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Project successfully updated",
    "project": {
        "projectNum": "",
        "id": "",
        "title": "",
        "status": "",
        "clientId": "",
        "progression": "",
        "startDate": "",
        "deadline": "",
        "employees":  [""],
        "fixedRate": "",
        "hourlyRate": "",
        "estimateHour": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer un projet

---

**Route de suppression d'un projet par un employé ou un gérant.**

**URL** : `/project/:id`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID du projet à modifier | ✔️ |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Project successfully deleted",
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
### Tâches

#### Liste des tâches

---

**Route de récupération de la liste des tâches pour un projet.**

**URL** : `/task`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| - | - | - | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful tasks acquisition",
    "tasks": [{
        "name": "",
        "progression": "",
        "description": "",
        "projectId": "",
        "employees": [""],
        "startDate": "",
        "deadline": "",
        "estimateHour": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Créer une tâche

---

**Route de création d'une tâche par un employé ou un gérant.**

**URL** : `/task`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| name | string | Nom de la tâche | ✔️ | 
| progression | number | Progression de la tâche | ✔️ | 
| description | string | Description de la tâche | - | 
| projectId | string | ID du projet lié à la tâche | ✔️ | 
| employees | array | Liste des employés liés à la tâche | ✔️ | 
| startDate | date | Date de début de la tâche | ✔️ | 
| deadline | date | Date de fin de la tâche | ✔️ | 
| estimateHour | number | Nombre d'heures estimées | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Task successfully created", 
    "task": {
        "name": "",
        "progression": "",
        "description": "",
        "projectId": "",
        "employees": [""],
        "startDate": "",
        "deadline": "",
        "estimateHour": "",
    },
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer une tâche

---

**Route de suppression d'une tâche par un employé ou un gérant.**

**URL** : `/task/:id`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de la tâche à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Task successfully deleted"
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
### Temps

#### Liste des temps enregistrés

---

**Route de récupération de la liste des temps enregistrés pour un projet.**

**URL** : `/time`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| - | - | - | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful times acquisition",
    "times": [{
        "userId": "",
        "projectId": "",
        "taskId": "",
        "billable": "",
        "duration": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Créer un enregistrement de temps

---

**Route de création d'un enregistrement de temps par un employé ou un gérant.**

**URL** : `/time`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| userId | string | ID de l'employé ou le gérant enregistrant le temps | ✔️ | 
| taskId | string | ID de la tâche lié au temps enregistré | - | 
| projectId | string | ID du projet lié au temps enregistré | ✔️ | 
| billable | boolean | Booléen pour savoir si le temps est factirable ou non | ✔️ | 
| duration | number | Durée estimé de la tâche en heure | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Time successfully created", 
    "time": {
        "userId": "",
        "taskId": "",
        "projectId": "",
        "billable": "",
        "duration": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer un enregistrement de temps

---

**Route de suppression d'un enregistrement de temps par un employé ou un gérant.**

**URL** : `/time/:id`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID du temps à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Time successfully deleted"
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
### Dépenses

#### Liste des dépenses

---

**Route de récupération de la liste des dépenses pour un gérant ou un employé.**

**URL** : `/expense`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| - | - | - | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful expenses acquisition",
    "expenses": [{
        "expenseNum": "",
        "id": "",
        "price": "",
        "accountNumber": "",
        "category": "",
        "file": "",
        "description": "",
        "userId/idManager": "",
        "projectId": "",
        "invoiced": "",
        "createdAt": "",
        "updatedAt": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Créer une dépense

---

**Route de création d'une note de frais pour les employés et les gérants.**

**URL** : `/expense-employee`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| expenseNum | string | Numéro unique de dépense | ✔️ | 
| userId/idManager | string | ID de l'employé ou du gérant créant la dépense | ✔️ | 
| projectId | string | ID du projet lié à la dépense | ✔️ | 
| price | number | Montant de la dépense  | ✔️ | 
| accountNumber | number | Numéro de compte comptable de la dépense | ✔️ | 
| category | string | Category de dépense | ✔️ | 
| invoiced | boolean | Booléen pour savoir si la dépense est facturé ou non | ✔️ | 
| file | file | Document de justification de la dépense | - | 
| description | string | Description de la dépense | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Expense successfully created", 
    "expense": {
        "expenseNum": "",
        "id": "",
        "price": "",
        "accountNumber": "",
        "category": "",
        "file": "",
        "description": "",
        "userId/idManager": "",
        "projectId": "",
        "invoiced": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer une dépense

---

**Route de suppression d'une dépense par un employé ou un gérant.**

**URL** : `/expense/:id`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de la dépense à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Expense successfully deleted"
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
### Conversations

#### Liste des conversations

---

**Route de récupération de la liste des conversation d'un utilisateur.**

**URL** : `/conversations`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| - | - | - | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful conversation acquisition",
    "conversations": [{
        "id": "",
        "idUser": "",
        "idUser1": "",
        "createdAt": "",
        "updatedAt": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Créer une conversation

---

**Route de création d'une conversation par un utilisateur.**

**URL** : `/conversation`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| idUser | string | ID du premier utilisateur de la conversation | ✔️ |
| idUser1 | string | ID du second utilisateur de la conversation | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Conversation successfully created",
    "conversation": {
        "id": "",
        "idUser": "",
        "idUser1": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer une conversation

---

**Route de suppression d'une conversation par un utilisateur.**

**URL** : `/conversation/:id`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de la conversation à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Chat successfully deleted"
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Liste des messages

---

**Route de récupération de la liste des messages pour une conversation.**

**URL** : `/conversation/messages/:id`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| - | - | - | - | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful messages acquisition",
    "conversations": [{
        "id": "",
        "idUser": "",
        "idConversation": "",
        "text": "",
        "createdAt": "",
        "updatedAt": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Unauthorized to access to this resource"
}
```

### Paiement
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Effectuer un paiement

---

**Route pour effectuer un paiement.**

**URL** : ``

**Methode** : ``

**Token requis** : ``

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| xxxx | xxxx | xxxx | xxxx | 
| xxxx | xxxx | xxxx | xxxx | 
| xxxx | xxxx | xxxx | xxxx | 
| xxxx | xxxx | xxxx | xxxx | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false
}
```

##### Requête échouée

**Condition** : 

**Code** : `400`

```json
{
    "error": true,
    "code": "",
    "message": ""
}
```

---

### Statistiques
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Obtenir les statistiques

---

**Route de récupération des statistiques pour la page d'accueil.**

**URL** : ``

**Methode** : ``

**Token requis** : ``

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| xxxx | xxxx | xxxx | xxxx | 
| xxxx | xxxx | xxxx | xxxx | 
| xxxx | xxxx | xxxx | xxxx | 
| xxxx | xxxx | xxxx | xxxx | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false
}
```

##### Requête échouée

**Condition** : 

**Code** : `400`

```json
{
    "error": true,
    "code": "",
    "message": ""
}
```
---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
