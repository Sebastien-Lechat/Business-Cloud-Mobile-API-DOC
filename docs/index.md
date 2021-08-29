# Bienvenue sur la documentation de l'API Business Cloud Mobile

Vous trouverez ici, l'ensemble de la documentation relative à l'API.

## Intallation de l'API en local

* `Récupération du projet` - [Lien du GitHub](https://github.com/Sebastien-Lechat/Business-Cloud-Mobile-API).
* `Exécution de commande` - Ensemble des commandes nécessaire à exécuter pour le lancement du projet.

```
npm install
npm start
```
* `Lancement du serveur` - Le serveur est lancé à l'adresse suivante : [http://localhost:8081/](http://localhost:8081/)

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
        "country" : "",
        "token" : "",
        "refreshToken" : "",
        "createdAt" : "",
        "updatedAt" : "",
        "userId": "",
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
    "message": "Missing email or password field"
}
```

**Condition** : Adresse email invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "101002",
    "message": "Invalid email addresse"
}
```

**Condition** : Mauvaise information de connexion.

**Code** : `400`

```json
{
    "error": true,
    "code": "101003",
    "message": "Invalid login credential"
}
```

**Condition** : Si l'adresse email n'est pas encore vérifié.

**Code** : `400`

```json
{
    "error": true,
    "code": "101004",
    "message": "Email address is not verified"
}
```

**Condition** : Si la double authentification est activé mais que le code n'est pas fourni.

**Code** : `400`

```json
{
    "error": true,
    "code": "101005",
    "message": "Double authentification is activated, code is required"
}
```

**Condition** : Si le code de double authentification est faux.

**Code** : `400`

```json
{
    "error": true,
    "code": "101006",
    "message": "Wrong code"
}
```

**Condition** : Si le code de double authentification est expiré.

**Code** : `400`

```json
{
    "error": true,
    "code": "101007",
    "message": "This code is no longer valid"
}
```

**Condition** : Si le compte de l'utilisateur est désactivé.

**Code** : `400`

```json
{
    "error": true,
    "code": "101008",
    "message": "This account is disabled"
}
```

**Condition** : Trop de tentative de connexion sur ce mail.

**Code** : `400`

```json
{
    "error": true,
    "code": "101008",
    "message": "Too many attempts on this email (5 max) - Please wait (5min)"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Connexion à une API extérieur

---

**Route de connexion pour n'importe quel type d'utilisateur via une API externe.**

**URL** : `/auth/external/login`

**Methode** : `POST`

**Token requis** : `NON`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| id | string | ID du compte externe | ✔️ |
| type | string | Nom de l'API externe utilisé (facebook, google) | ✔️ |
| email | string | Email de l'utilisateur | ✔️ |
| token | string | Token fourni par l'API externe | ✔️ | 

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
        "country" : "",
        "token" : "",
        "refreshToken" : "",
        "createdAt" : "",
        "updatedAt" : "",
        "userId": "",
    }
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "101401",
    "message": "Missing email or password field"
}
```

**Condition** : Adresse email invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "101402",
    "message": "Invalid email addresse"
}
```

**Condition** : Aucun compte lié valide.

**Code** : `400`

```json
{
    "error": true,
    "code": "101403",
    "message": "No account linked to this email"
}
```

**Condition** : Le type ne correspond à aucun type valide.

**Code** : `400`

```json
{
    "error": true,
    "code": "101404",
    "message": "Invalid type"
}
```

**Condition** : ID de compte extérieur invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "101405",
    "message": "Invalid external account ID"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->

#### Inscription

---

**Route de d'inscription d'un utilisateur (client ou entreprise).**

**URL** : `/auth/register`

**Methode** : `POST`

**Token requis** : `NON`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| name | string | Nom et prénom du client ou de l'entreprise | ✔️ | 
| email | string | Email du client ou de l'entreprise | ✔️ | 
| phone | string | Téléphone du client ou de l'entreprise | - |
| password | string | Mot de passe du client ou de l'entreprise | ✔️ | 
| address | string | Adresse du client ou de l'entreprise | ✔️ |
| zip | string | Code postal du client ou de l'entreprise | ✔️ |
| city | string | Ville du client ou de l'entreprise | ✔️ |
| country | string | Pays du client ou de l'entreprise | ✔️ |
| numTVA | string | Numéro de TVA de l'entreprise | ✔️ |
| numSIRET | string | Numéro de SIRET de l'entreprise | ✔️ |
| numRCS | string | Numéro de RCS de l'entreprise | ✔️ |

##### Requête réussie

**Code** : `201`

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

**Condition** : Adresse email invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "101052",
    "message": "Invalid email addresse"
}
```

**Condition** : Numéro de téléphone invalide (format invalide).

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

**Condition** : L'email est déjà utilisé par un autre utilisateur.

**Code** : `400`

```json
{
    "error": true,
    "code": "101058",
    "message": "This email is already used"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Mot de passe oublié

---

**Route de récupération du mot depasse utilisateur. Le mail contient un lien de redirection sur le site pour modifier le mot de passe.**

**URL** : `/auth/request-password-lost`

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

**Condition** : Champ email manquant.

**Code** : `400`

```json
{
    "error": true,
    "code": "101101",
    "message": "Missing email field"
}
```

**Condition** : Adresse email invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "101102",
    "message": "Invalid email addresse"
}
```

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

**Condition** : Champ email manquant.

**Code** : `400`

```json
{
    "error": true,
    "code": "101151",
    "message": "Missing email field"
}
```

**Condition** : Adresse email invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "101152",
    "message": "Invalid email addresse"
}
```

**Condition** : Email déjà vérifié.

**Code** : `400`

```json
{
    "error": true,
    "code": "101153",
    "message": "Email already verified"
}
```

**Condition** : Echec de l'envoi du mail.

**Code** : `500`

```json
{
    "error": true,
    "code": "500002",
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

**Condition** : Champ email ou code manquant.

**Code** : `400`

```json
{
    "error": true,
    "code": "101201",
    "message": "Missing email or code field"
}
```

**Condition** : Adresse email invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "101202",
    "message": "Invalid email addresse"
}
```

**Condition** : Code ou adresse email invalide (utilisateur introuvable).

**Code** : `400`

```json
{
    "error": true,
    "code": "101203",
    "message": "Invalid user information"
}
```

**Condition** : L'email n'est pas en court de vérification.

**Code** : `400`

```json
{
    "error": true,
    "code": "101204",
    "message": "You need to make a request to check this email"
}
```

**Condition** : Mauvais code.

**Code** : `400`

```json
{
    "error": true,
    "code": "101205",
    "message": "Wrong code"
}
```

**Condition** : Code expiré.

**Code** : `400`

```json
{
    "error": true,
    "code": "101206",
    "message": "This code is no longer valid"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Double authentification (envoi)

---

**Route d'envoi d'un email contenant un code de vérification à un utilisateur lors de sa connexion, si la double authentification est activé.**

**URL** : `/auth/request-double-auth`

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

**Condition** : Champ email manquant.

**Code** : `400`

```json
{
    "error": true,
    "code": "101251",
    "message": "Missing email"
}
```

**Condition** : Adresse email invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "101252",
    "message": "Invalid email addresse"
}
```

**Condition** : ID ou adresse email invalide (utilisateur introuvable).

**Code** : `400`

```json
{
    "error": true,
    "code": "101253",
    "message": "Invalid user information"
}
```

**Condition** : Double authentification désactivé.

**Code** : `400`

```json
{
    "error": true,
    "code": "101254",
    "message": "Double authentification is not activated on this account"
}
```

**Condition** : Echec de l'envoi du mail.

**Code** : `500`

```json
{
    "error": true,
    "code": "500003",
    "message": "Internal server error, email can not be send"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Double authentification (activation)

---

**Route d'activation de la double authentification pour un utilisateur.**

**URL** : `/auth/active-double-auth`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| isActive | boolean | Booléen pour définir si la double authentification est actié ou non | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Double authentification successfully updated"
}
```

##### Requête échouée

**Condition** : Champ isActive manquant.

**Code** : `400`

```json
{
    "error": true,
    "code": "101301",
    "message": "Missing isActive field"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Déconnexion

---

**Route de déconnexion pour n'importe quel type d'utilisateur.**

**URL** : `/auth/disconnect`

**Methode** : `DELETE`

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
    "message": "Successfully logout"
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
        "needVerifyEmail": "",
    }
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modification des informations personnelles

---

**Route de modification des informations personnelles, des informations de contact.**

**URL** : `/account/information`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| name | string | Nom et prénom de l'utilisateur ou de l'entreprise | - | 
| email | string | Email de l'utilisateur ou de l'entreprise | - | 
| phone | string | Téléphone de l'utilisateur ou de l'entreprise | - |

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
        "needVerifyEmail": "",
    }
}
```

##### Requête échouée

**Condition** : Adresse email invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "102051",
    "message": "Invalid email addresse"
}
```

**Condition** : Numéro de téléphone invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "102052",
    "message": "Invalid phone number"
}
```

**Condition** : Date de naisseance invalide (DD-MM-YYY).

**Code** : `400`

```json
{
    "error": true,
    "code": "102053",
    "message": "Invalid date format"
}
```

**Condition** : L'email est déjà utilisé par un autre utilisateur.

**Code** : `400`

```json
{
    "error": true,
    "code": "102054",
    "message": "This email is already used"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modification de l'avatar

---

**Route de modification de l'avatar de l'utilisateur.**

**URL** : `/account/avatar`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| avatarPath | string | nom du fichier pour la récupération sur firecloud storage | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Profile successfully updated",
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "102301",
    "message": "Missing important fields"
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
        "needVerifyEmail": "",
    }
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "102101",
    "message": "Missing important fields"
}
```

**Condition** : Ancien mot de passe invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "102102",
    "message": "Invalid old password"
}
```

**Condition** : Nouveau mot de passe invalide ou à faible sécurité.

**Code** : `400`

```json
{
    "error": true,
    "code": "102103",
    "message": "Invalid password format"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modification de l'adresse

---

**Route de modification des information de location de l'utilisateur.**

**URL** : `/account/address`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| address | string | Adresse de l'utilisateur ou de l'entreprise | - |
| zip | string | Code postal de l'utilisateur ou de l'entreprise | - |
| city | string | Ville de l'utilisateur ou de l'entreprise | - |
| country | string | Pays de l'utilisateur ou de l'entreprise | - |

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
        "needVerifyEmail": "",
    }
}
```

##### Requête échouée

**Condition** : Si l'utilisateur faisant la requête n'est ni gérant, ni un client.

**Code** : `400`

```json
{
    "error": true,
    "code": "102151",
    "message": "You cannot edit your address with this account"
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
| activity | string | Activité de l'entreprise | - |
| numTVA | string | Numéro de TVA de l'entreprise | - |
| numSIRET | string | Numéro de SIRET de l'entreprise | - |
| numRCS | string | Numéro de RCS de l'entreprise | - |
<!-- | currency | string | Monnaie avec laquelle les factures seront générées pour le client | - | -->

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
        "needVerifyEmail": "",
    }
}
```

##### Requête échouée

**Condition** : Si l'utilisateur faisant la requête n'est ni gérant, ni un client.

**Code** : `400`

```json
{
    "error": true,
    "code": "102201",
    "message": "You cannot edit your enterprise with this account"
}
```

**Condition** : Numéro de TVA invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "102202",
    "message": "Invalid TVA number"
}
```

**Condition** : Numéro de SIRET invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "102203",
    "message": "Invalid SIRET number"
}
```

**Condition** : Numéro de RCS invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "102204",
    "message": "Invalid RCS number"
}
```
---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->

#### Enregistrement d'un appareil

---

**Route d'enregistrement pour l'envoi de notification avec firebase**

**URL** : `/account/register-fcm`

**Methode** : `PUT`

**Token requis** : `NON`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| deviceId | string | ID de l'appareil | ✔️ | 
| token | string | Token d'authentification pour l'enregistrement donné par firebase | ✔️ | 


##### Requête réussie

**Code** : `201`

```json
{
    "error": false,
    "message": "Device successfully added"
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "102251",
    "message": "Missing important fields"
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

**Condition** : Id utilisateur manquant.

**Code** : `400`

```json
{
    "error": true,
    "code": "103101",
    "message": "Missing id field"
}
```

**Condition** : Id utilisateur invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103102",
    "message": "Invalid user id"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Récupération de l'historique

---

**Route de récupération de l'historique d'un utilisateur.**

**URL** : `/user/history/:id`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| id | string | ID de l'utilisateur ciblé | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful history acquisition",
    "history" : [{
        "_id":"",
        "action": {
            "method": "",
            "route": "",
        },
        "userEmail": "",
        "success": "",
        "createdAt": "",
        "updatedAt": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : Id utilisateur manquant.

**Code** : `400`

```json
{
    "error": true,
    "code": "103451",
    "message": "Missing id field"
}
```

**Condition** : Id utilisateur invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103452",
    "message": "Invalid user id"
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
| name | string | Nom et prénom du client ou de l'entreprise | ✔️ | 
| email | string | Email du client ou de l'entreprise | ✔️ | 
| password | string | Mot de passe du client ou de l'entreprise | ✔️ | 
| phone | string | Téléphone du client ou de l'entreprise | - |
| address | string | Adresse du client ou de l'entreprise | - |
| zip | string | Code postal du client ou de l'entreprise | - |
| city | string | Ville du client ou de l'entreprise | - |
| country | string | Pays du client ou de l'entreprise | - |
| numTVA | string | Numéro de TVA de l'entreprise | - |
| numSIRET | string | Numéro de SIRET de l'entreprise | - |
| numRCS | string | Numéro de RCS de l'entreprise | - |
<!-- | currency | string | Monnaie avec laquelle les factures seront générée pour le client | - | -->
| note | string | Annotation sur le client sur le client | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Customer successfully created",
    "customer": {
        "id":"",
        "userId": "",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "type" : "",
        "address" : "",
        "zip" : "",
        "city" : "",
        "country" : "",
        "activity" : "",
        "numTVA" : "",
        "numSIRET" : "",
        "numRCS" : "",
        "createdAt" : "",
        "updatedAt" : "",
    }
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "103151",
    "message": "Missing important fields"
}
```

**Condition** : Adresse email invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "103152",
    "message": "Invalid email addresse"
}
```

**Condition** : Numéro de téléphone invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "103153",
    "message": "Invalid phone number"
}
```

**Condition** : Mot de passe invalide ou à faible sécurité.

**Code** : `400`

```json
{
    "error": true,
    "code": "103154",
    "message": "Invalid password format"
}
```

**Condition** : Numéro de TVA invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103155",
    "message": "Invalid TVA number"
}
```

**Condition** : Numéro de SIRET invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103156",
    "message": "Invalid SIRET number"
}
```

**Condition** : Numéro de RCS invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103157",
    "message": "Invalid RCS number"
}
```

**Condition** : L'email est déjà utilisé par un autre utilisateur.

**Code** : `400`

```json
{
    "error": true,
    "code": "103158",
    "message": "This email is already used"
}
```

**Condition** : Id employé invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103159",
    "message": "Invalid employee id"
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
| name | string | Nom et prénom du client ou de l'entreprise | - | 
| email | string | Email du client ou de l'entreprise | - | 
| phone | string | Téléphone du client ou de l'entreprise | - |
| address | string | Adresse du client ou de l'entreprise | - |
| zip | string | Code postal du client ou de l'entreprise | - |
| city | string | Ville du client ou de l'entreprise | - |
| country | string | Pays du client ou de l'entreprise | - |
| numTVA | string | Numéro de TVA de l'entreprise | - |
| numSIRET | string | Numéro de SIRET de l'entreprise | - |
| numRCS | string | Numéro de RCS de l'entreprise | - |
<!-- | currency | string | Monnaie avec laquelle les factures seront générées pour le client | - | -->
| note | string | Annotation sur le client sur le client | - |


##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Customer successfully updated",
    "user": {
        "id":"",
        "userId": "",
        "avatar" : "",
        "name" : "",
        "email" : "",
        "phone" : "",
        "type" : "",
        "address" : "",
        "zip" : "",
        "city" : "",
        "country" : "",
        "activity" : "",
        "numTVA" : "",
        "numSIRET" : "",
        "numRCS" : "",
        "createdAt" : "",
        "updatedAt" : "",
    }
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "103201",
    "message": "Missing id field"
}
```

**Condition** : Adresse email invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "103202",
    "message": "Invalid email addresse"
}
```

**Condition** : Numéro de téléphone invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "103203",
    "message": "Invalid phone number"
}
```

**Condition** : Id du client invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103204",
    "message": "Invalid customer id"
}
```

**Condition** : Numéro de TVA invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103205",
    "message": "Invalid TVA number"
}
```

**Condition** : Numéro de SIRET invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103206",
    "message": "Invalid SIRET number"
}
```

**Condition** : Numéro de RCS invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103207",
    "message": "Invalid RCS number"
}
```

**Condition** : L'email est déjà utilisé par un autre utilisateur.

**Code** : `400`

```json
{
    "error": true,
    "code": "103208",
    "message": "This email is already used"
}
```

**Condition** : Id employé invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103209",
    "message": "Invalid employee id"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer un client

---

**Route de suppression d'un client par un employé ou un gérant. La requête ne supprimera pas réellement l'utilisateur, elle le désactivera seulement.**

**URL** : `/customer/:id`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID du client à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Customer successfully deleted"
}
```

##### Requête échouée

 **Condition** : Champs obligatoires manquants.
 
**Code** : `400`

```json
{
    "error": true,
    "code": "103251",
    "message": "Missing id field"
}
```

 **Condition** : Id du client invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103252",
    "message": "Invalid customer id"
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
| name | string | Nom et prénom de l'employé | ✔️ | 
| email | string | Email de l'employé | ✔️ | 
| phone | string | Téléphone de l'employé | - |
| password | string | Mot de passe de l'employé | ✔️ | 
| role | string | Rôle de l'employé au sein de l'entreprise | ✔️ |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Employee successfully created",
    "employee": {
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

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "103301",
    "message": "Missing important fields"
}
```

**Condition** : Adresse email invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "103302",
    "message": "Invalid email addresse"
}
```

**Condition** : Numéro de téléphone invalide (format invalide).

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
    "message": "Invalid password format"
}
```

**Condition** : Rôle invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "103305",
    "message": "Invalid enterprise role"
}
```

**Condition** : L'email est déjà utilisé par un autre utilisateur.

**Code** : `400`

```json
{
    "error": true,
    "code": "103306",
    "message": "This email is already used"
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
| name | string | Nom et prénom de l'employé | - | 
| email | string | Email de l'employé | - | 
| phone | string | Téléphone de l'employé | - |
| role | string | Rôle de l'employé au sein de l'entreprise | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Employee successfully updated",
    "employee": {
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

**Condition** : Champs obligatoires manquants.
 
**Code** : `400`

```json
{
    "error": true,
    "code": "103351",
    "message": "Missing id field"
}
```

**Condition** : Adresse email invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "103352",
    "message": "Invalid email addresse"
}
```

**Condition** : Numéro de téléphone invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "103353",
    "message": "Invalid phone number"
}
```

**Condition** : Id de l'employé invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103354",
    "message": "Invalid employee id"
}
```

**Condition** : Rôle invalide (format invalide).

**Code** : `400`

```json
{
    "error": true,
    "code": "103355",
    "message": "Invalid enterprise role"
}
```

**Condition** : L'email est déjà utilisé par un autre utilisateur.

**Code** : `400`

```json
{
    "error": true,
    "code": "103356",
    "message": "This email is already used"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer un employé

---

**Route de suppression d'un employé par un gérant. La requête ne supprimera pas réellement l'employé, elle le désactivera seulement.**

**URL** : `/employee/:id`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de l'employé à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Employee successfully deleted"
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.
 
**Code** : `400`

```json
{
    "error": true,
    "code": "103401",
    "message": "Missing id field"
}
```

 **Condition** : Id de l'employé invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "103402",
    "message": "Invalid employee id"
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

**Condition** : ID de facture invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104101",
    "message": "Invalid bill id"
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
<!-- | currency | string | Monnaie avec laquelle la facture sera généré | ✔️ | -->
| deadline | date | Date limite à laquelle le client peut payer la facture | ✔️ |

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
        "totalHT": "",
        "totalTTC": "",
        "deadline": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "104151",
    "message": "Missing important fields"
}
```

**Condition** : Statut de facture invalide (Non payée, Partiellement payée, Payée, En retard).

**Code** : `400`

```json
{
    "error": true,
    "code": "104152",
    "message": "Invalid bill status"
}
```

**Condition** : Id du client invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104153",
    "message": "Invalid customer id"
}
```

**Condition** : ID de l'entreprise invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104154",
    "message": "Invalid enterprise id"
}
```

**Condition** : Numéro de facture invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104155",
    "message": "Invalid bill number"
}
```

**Condition** : Date d'échéance invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104156",
    "message": "Invalid deadline"
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
<!-- | currency | string | Monnaie avec laquelle la facture sera généré | - | -->
| deadline | date | Date limite à laquelle le client peut payer la facture | - |

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

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "104201",
    "message": "Missing important fields"
}
```

**Condition** : Statut de facture invalide (Non payée, Partiellement payée, Payée, En retard).

**Code** : `400`

```json
{
    "error": true,
    "code": "104202",
    "message": "Invalid bill status"
}
```

**Condition** : Id du client invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104203",
    "message": "Invalid customer id"
}
```

**Condition** : ID de l'entreprise invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104204",
    "message": "Invalid enterprise id"
}
```

**Condition** : Numéro de facture invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104205",
    "message": "Invalid bill number"
}
```

**Condition** : Date d'échéance invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104206",
    "message": "Invalid deadline"
}
```

**Condition** : Format de l'article invalide (ID ou quantité manquante).

**Code** : `400`

```json
{
    "error": true,
    "code": "104207",
    "message": "Invalid article format"
}
```

**Condition** : ID d'un article invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104208",
    "message": "Some article id are invalid"
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
| :id | string | ID de la facture à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Bill successfully deleted"
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "104251",
    "message": "Missing id field"
}
```

**Condition** : ID de facture invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104252",
    "message": "Invalid bill id"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Relancer un client sur une facture

---

**Route d'envoi d'un email et d'une notification pour la relance sur le payement d'une facture.**

**URL** : `/bill/:billId/customer/:clientId/mail`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| billId | string | ID de la facture | ✔️ | 
| clientId | string | ID du client lié à la facture | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Mail successfully send"
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "104301",
    "message": "Missing important fields"
}
```

**Condition** : Id de la facture invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104302",
    "message": "Invalid bill id"
}
```

**Condition** : Id du client invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104153",
    "message": "Invalid customer id"
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
        "totalHT": "",
        "totalTTC": "",
        "deadline": "",
        "createdAt": "",
        "updatedAt": "",
    },{...}]
}
```

##### Requête échouée

 

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
        "totalHT": "",
        "totalTTC": "",
        "deadline": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```

##### Requête échouée

**Condition** : ID de devis invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105101",
    "message": "Invalid estimate id"
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
| deadline | date | Date limite à laquelle le client peut accepter le devis | ✔️ |

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
        "totalHT": "",
        "totalTTC": "",
        "deadline": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "105151",
    "message": "Missing important fields"
}
```

**Condition** : Statut du devis invalide (En attente, Refusé, Accepté, En retard).

**Code** : `400`

```json
{
    "error": true,
    "code": "105152",
    "message": "Invalid estimate status"
}
```

**Condition** : ID du client invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105153",
    "message": "Invalid customer id"
}
```

**Condition** : ID de l'entreprise invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105154",
    "message": "Invalid enterprise id"
}
```

**Condition** : Numéro de devis invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105155",
    "message": "Invalid estimate number"
}
```

**Condition** : Date d'échéance invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105156",
    "message": "Invalid deadline"
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
| deadline | date | Date limite à laquelle le client peut payer le devis | - |

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

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "105201",
    "message": "Missing important fields"
}
```

**Condition** : Statut du devis invalide (En attente, Refusé, Accepté, En retard).

**Code** : `400`

```json
{
    "error": true,
    "code": "105202",
    "message": "Invalid estimate status"
}
```

**Condition** : Id du client invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105203",
    "message": "Invalid customer id"
}
```

**Condition** : ID de l'entreprise invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105204",
    "message": "Invalid enterprise id"
}
```

**Condition** : Numéro de devis invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105205",
    "message": "Invalid estimate number"
}
```

**Condition** : Date d'échéance invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105206",
    "message": "Invalid deadline"
}
```

**Condition** : Format de l'article invalide (ID ou quantité manquante).

**Code** : `400`

```json
{
    "error": true,
    "code": "105207",
    "message": "Invalid article format"
}
```

**Condition** : ID d'un article invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105208",
    "message": "Some article id are invalid"
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

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "105251",
    "message": "Missing id field"
}
```

**Condition** : ID de devis invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105252",
    "message": "Invalid estimate id"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Relancer un client sur un devis

---

**Route d'envoi d'un email et d'une notification pour la relance de l'acceptation d'un devis.**

**URL** : `/estimate/:estimateId/customer/:clientId/mail`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| estimateId | string | ID du devis | ✔️ | 
| clientId | string | ID du client lié au devis | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Mail successfully send"
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "105301",
    "message": "Missing important fields"
}
```

**Condition** : Id du devis invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105302",
    "message": "Invalid estimate id"
}
```

**Condition** : Id du client invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105303",
    "message": "Invalid customer id"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Transformer un devis en facture

---

**Route de transformation d'un devis en une facture en respectant les articles.**

**URL** : `/estimate/:estimateId/customer/:clientId/mail`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| estimateId | string | ID du devis | ✔️ | 
| clientId | string | ID du client lié au devis | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Mail successfully send"
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "105351",
    "message": "Missing important fields"
}
```

**Condition** : Id du devis invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105352",
    "message": "Invalid estimate id"
}
```

**Condition** : Id du client invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "105353",
    "message": "Invalid customer id"
}
```

**Condition** : Statut du devis invalide (déjà accepté).

**Code** : `400`

```json
{
    "error": true,
    "code": "105354",
    "message": "Invalid estimate status"
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
        "_id": "",
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
        "_id": "",
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

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "106101",
    "message": "Missing important fields"
}
```

**Condition** : Numéro de compte invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "106102",
    "message": "Invalid account number"
}
```

**Condition** : Format du prix invalide (Float).

**Code** : `400`

```json
{
    "error": true,
    "code": "106103",
    "message": "Invalid price format"
}
```

**Condition** : Format de la taxe invalide (Float).

**Code** : `400`

```json
{
    "error": true,
    "code": "106104",
    "message": "Invalid tva format"
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

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "106151",
    "message": "Missing id field"
}
```

**Condition** : ID de l'article invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "106152",
    "message": "Invalid article id"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
### Projets

#### Liste des projets

---

**Route de récupération de la liste des projets pour un employé ou un gérant.**

**URL** : `/projects`

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

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Récupération d'un projet

---

**Route de récupération d'un projet pour un employé ou un gérant.**

**URL** : `/project/:id`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID du projet à récupérer | ✔️ |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful project acquisition",
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
    }]
}

```
##### Requête échouée

 **Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "108101",
    "message": "Missing id field"
}
```

**Condition** : ID du projet invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108102",
    "message": "Invalid project id"
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

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "108151",
    "message": "Missing important fields"
}
```

**Condition** : Statut du projet invalide (En attente, En cours, Terminé, En retard).

**Code** : `400`

```json
{
    "error": true,
    "code": "108152",
    "message": "Invalid project status"
}
```

**Condition** : ID du client invalid.

**Code** : `400`

```json
{
    "error": true,
    "code": "108153",
    "message": "Invalid customer id"
}
```

**Condition** : Numéro de projet invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108154",
    "message": "Invalid project number"
}
```

**Condition** : Numéro de progression invalide (0-100).

**Code** : `400`

```json
{
    "error": true,
    "code": "108155",
    "message": "Invalid progression number"
}
```

**Condition** : Date d'échéance invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108156",
    "message": "Invalid deadline"
}
```

**Condition** : Si un ID employé est invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108157",
    "message": "Some employee id are invalid"
}
```

**Condition** : Si le taux horaire et le taux fixe sont renseigné en même temps.

**Code** : `400`

```json
{
    "error": true,
    "code": "108158",
    "message": "You can't have both billing systems active"
}
```

**Condition** : Format de taxe fixe invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108159",
    "message": "Invalid fixed rate"
}
```

**Condition** : Format de taxe horaire invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108160",
    "message": "Invalid hourly rate"
}
```

**Condition** : Format du temps estimé invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108161",
    "message": "Invalid estimate hour"
}
```

**Condition** : Date de début situé après la date d'échéance.

**Code** : `400`

```json
{
    "error": true,
    "code": "108162",
    "message": "Start date can't be set after deadline"
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

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "108201",
    "message": "Missing id field"
}
```

**Condition** : Statut du projet invalide (En attente, En cours, Terminé, En retard).

**Code** : `400`

```json
{
    "error": true,
    "code": "108202",
    "message": "Invalid project status"
}
```

**Condition** : ID du client invalid.

**Code** : `400`

```json
{
    "error": true,
    "code": "108203",
    "message": "Invalid customer id"
}
```

**Condition** : Numéro de projet invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108204",
    "message": "Invalid project number"
}
```

**Condition** : Numéro de progression invalide (0-100).

**Code** : `400`

```json
{
    "error": true,
    "code": "108205",
    "message": "Invalid progression number"
}
```

**Condition** : Date d'échéance invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108206",
    "message": "Invalid deadline"
}
```

**Condition** : Si un ID employé est invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108207",
    "message": "Some employee id are invalid"
}
```

**Condition** : Si le taux horaire et le taux fixe sont renseigné en même temps.

**Code** : `400`

```json
{
    "error": true,
    "code": "108208",
    "message": "You can't have both billing systems active"
}
```

**Condition** : Format de taxe fixe invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108209",
    "message": "Invalid fixed rate"
}
```

**Condition** : Format de taxe horaire invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108210",
    "message": "Invalid hourly rate"
}
```

**Condition** : Format du temps estimé invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108211",
    "message": "Invalid estimate hour"
}
```

**Condition** : Date de début situé après la date d'échéance.

**Code** : `400`

```json
{
    "error": true,
    "code": "108212",
    "message": "Start date can't be set after deadline"
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
| :id | string | ID du projet à supprimer | ✔️ |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Project successfully deleted",
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "108251",
    "message": "Missing id field"
}
```

**Condition** : ID du projet invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108252",
    "message": "Invalid project id"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Transformer un projet en facture

---

**Route de transformation d'un projet par un employé ou un gérant.**

**URL** : `/project/transform/:id`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID du projet à transformer | ✔️ |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Project successfully transformed",
    "billId": "",
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "108301",
    "message": "Missing id field"
}
```

**Condition** : ID du projet invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "108302",
    "message": "Invalid project id"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
### Temps

#### Liste des temps enregistrés

---

**Route de récupération de la liste des temps enregistrés pour un projet.**

**URL** : `/times`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID du projet pour lequel on veut récupérer les temps | - |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful times acquisition",
    "times": [{
        "id": "",
        "userId": "",
        "projectId": "",
        "taskName": "",
        "billable": "",
        "duration": "",
        "createdAt": "",
        "updatedAt": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : ID du projet invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "110051",
    "message": "Invalid project id"
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
| taskName | string | Nom de la tâche liée au temps | - | 
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
        "id": "",
        "userId": "",
        "taskName": "",
        "projectId": "",
        "billable": "",
        "duration": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "110101",
    "message": "Missing important fields"
}
```

**Condition** : ID de projet invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "110102",
    "message": "Invalid project id"
}
```

**Condition** : ID de la tâche invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "110103",
    "message": "Invalid task id"
}
```

**Condition** : Format du champs facturable invalide (booléen).

**Code** : `400`

```json
{
    "error": true,
    "code": "110104",
    "message": "Invalid billable format"
}
```

**Condition** : Format de la durée invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "110105",
    "message": "Invalid duration number"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modifier un enregistrement de temps

---

**Route de modification d'un enregistrement de temps par un employé ou un gérant.**

**URL** : `/time`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| id | string | ID du temps enregistré | ✔️ | 
| billable | boolean | Booléen pour savoir si le temps est factirable ou non | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Time successfully updated", 
    "time": {
        "id": "",
        "userId": "",
        "taskName": "",
        "projectId": "",
        "billable": "",
        "duration": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "110151",
    "message": "Missing important fields"
}
```

**Condition** : ID du temps invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "110152",
    "message": "Invalid time id"
}
```

**Condition** : Format du champs facturable invalide (booléen).

**Code** : `400`

```json
{
    "error": true,
    "code": "110153",
    "message": "Invalid billable format"
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

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "110201",
    "message": "Missing id field"
}
```

**Condition** : ID du temps invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "110202",
    "message": "Invalid time id"
}
```


---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
### Dépenses

#### Liste des dépenses

---

**Route de récupération de la liste des dépenses pour un gérant ou un employé.**

**URL** : `/expenses/:projectId`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| projectId | string | ID du projet pour lequel on veut récupérer les dépenses | - |

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
        "userId": "",
        "projectId": "",
        "billable": "",
        "createdAt": "",
        "updatedAt": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : ID du projet invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "111001",
    "message": "Invalid project id"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Récupération d'une dépense

---

**Route de récupération d'une dépense pour un gérant ou un employé.**

**URL** : `/expense/:id`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de la dépense que l'on veut récupérer | ✔️ |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful expense acquisition",
    "expense": {
        "expenseNum": "",
        "id": "",
        "price": "",
        "accountNumber": "",
        "category": "",
        "file": "",
        "description": "",
        "userId": "",
        "projectId": "",
        "billable": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```
##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "111051",
    "message": "Missing id field"
}
```

**Condition** : ID de la dépense invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "111052",
    "message": "Invalid expense id"
}
```

---
<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->

#### Créer une dépense

---

**Route de création d'une note de frais pour les employés et les gérants.**

**URL** : `/expense`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| expenseNum | string | Numéro unique de dépense | ✔️ | 
| projectId | string | ID du projet lié à la dépense | ✔️ | 
| price | number | Montant de la dépense  | ✔️ | 
| accountNumber | number | Numéro de compte comptable de la dépense | ✔️ | 
| category | string | Category de dépense | ✔️ | 
| billable | boolean | Booléen pour savoir si la dépense est facturé ou non | ✔️ | 
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
        "userId": "",
        "projectId": "",
        "billable": "",
        "createdAt": "",
        "updatedAt": "",
    }
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "111101",
    "message": "Missing important fields"
}
```

**Condition** : Numéro de note de frais invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "111102",
    "message": "Invalid expense number"
}
```

**Condition** : Numéro de compte invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "111103",
    "message": "Invalid account number"
}
```

**Condition** : Format du prix invalide (Float).

**Code** : `400`

```json
{
    "error": true,
    "code": "111104",
    "message": "Invalid price format"
}
```

**Condition** : Format du champ facturable invalide (booléen).

**Code** : `400`

```json
{
    "error": true,
    "code": "111105",
    "message": "Invalid invoiced format"
}
```

**Condition** : Id du projet invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "111106",
    "message": "Invalid project id"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Modifier une dépense

---

**Route de modification d'une dépense par un employé ou un gérant.**

**URL** : `/expense`

**Methode** : `PUT`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| id | string | ID de la dépense à modifier | ✔️ | 
| billable | boolean | Booléen pour savoir si la dépense est facturé ou non | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Expense successfully updated"
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "111151",
    "message": "Missing id field"
}
```

**Condition** : ID de la dépense invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "111152",
    "message": "Invalid expense id"
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

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "111201",
    "message": "Missing id field"
}
```

**Condition** : ID de la dépense invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "111202",
    "message": "Invalid expense id"
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
    "message": "Successful conversations acquisition",
    "conversations": [{
        "id": "",
        "member1": "",
        "member2": "",
        "createdAt": "",
        "updatedAt": "",
        "lastMessage": "",
    },{...}]
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Récupération d'une conversation

---

**Route de récupération d'une conversation avec un autre utilisateur.**

**URL** : `/conversation/:id`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| id | string | ID de la conversation | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful conversation acquisition",
    "conversation": {
        "id": "",
        "member1": "",
        "member2": "",
        "createdAt": "",
        "updatedAt": "",
        "lastMessage": "",
    }
}
```

##### Requête échouée

**Condition** : ID de la conversation manquante.

**Code** : `400`

```json
{
    "error": true,
    "code": "112201",
    "message": "Missing id field"
}
```

**Condition** : ID de la conversation invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "112202",
    "message": "Invalid conversation id"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Récupération des messages d'une conversation

---

**Route de récupération des messages d'une conversation avec un autre utilisateur.**

**URL** : `/conversation/:id/messages`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| id | string | ID de la conversation | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful conversation messages acquisition",
    "messages": [{
        "conversationId": "",
        "userId": "",
        "text": "",
        "createdAt": "",
        "updatedAt": "",
    },{...}]
}
```

##### Requête échouée

**Condition** : ID de la conversation manquante.

**Code** : `400`

```json
{
    "error": true,
    "code": "112251",
    "message": "Missing id field"
}
```

**Condition** : ID de la conversation invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "112252",
    "message": "Invalid conversation id"
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
| userId | string | ID de l' utilisateur avec lequel on veut créer une conversation | ✔️ |

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Conversation successfully created",
    "conversation": {
        "id": "",
        "member1": "",
        "member2": "",
        "createdAt": "",
        "updatedAt": "",
        "lastMessage": "",
    }
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "112101",
    "message": "Missing important fields"
}
```

**Condition** : Si l'on créer une conversation avec soit même

**Code** : `400`

```json
{
    "error": true,
    "code": "112102",
    "message": "Can't create conversation with yourself"
}
```

**Condition** : ID de l'utilisateur invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "112103",
    "message": "Invalid user id"
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
    "message": "Conversation successfully deleted"
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "112151",
    "message": "Missing id field"
}
```

**Condition** : ID de la conversation invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "112152",
    "message": "Invalid conversation id"
}
```

---


<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
### Notifications

#### Liste des notifications

---

**Route de récupération de la liste des notifications d'un utilisateur.**

**URL** : `/notifications`

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
    "message": "Successful notifications acquisition",
    "conversations": [{
        "id": "",
        "title": "",
        "message": "",
        "catergory": "",
        "targetId": "",
        "userId": "",
        "seen": "",
        "createdAt": "",
        "updatedAt": "",
    },{...}]
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Compteur de notification

---

**Route de récupération du nombre de notifications non lu.**

**URL** : `/notifications/count`

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
    "message": "Successful notifications count acquisition",
    "count": "",
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Supprimer une notification

---

**Route de suppression d'une notification par un utilisateur.**

**URL** : `/notification/:id`

**Methode** : `DELETE`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de la notification à supprimer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Notification successfully deleted"
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "113101",
    "message": "Missing id field"
}
```

**Condition** : ID de la notification invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "113102",
    "message": "Invalid notification id"
}
```

---

### Paiement

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Génération des informations pour le paiement

---

**Route pour effectuer un paiement.**

**URL** : `/bill/payment-sheet`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| amount | number | montant à payer | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "paymentIntent": "",
    "ephemeralKey": "",
    "customer": ""
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "104351",
    "message": "Missing important fields"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Effectuer un paiement

---

**Route pour effectuer un paiement.**

**URL** : `/bill/payment/:id`

**Methode** : `POST`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | ID de la facture pour le paiement | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Bill successfully payed",

}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "104401",
    "message": "Missing important fields"
}
```

**Condition** : Id de la facture invalide.

**Code** : `400`

```json
{
    "error": true,
    "code": "104402",
    "message": "Invalid bill id"
}
```

**Condition** : Statut de la facture invalide (déjà payée).

**Code** : `400`

```json
{
    "error": true,
    "code": "104403",
    "message": "Invalid bill status"
}
```

---

### Statistiques

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Obtenir les statistiques

---

**Route de récupération des statistiques pour la page d'accueil.**

**URL** : `/global/statistics`

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
    "statistics": {
        "gainTotal": "",
        "expenseTotal": "",
        "employeeTotal": "",
        "customerTotal": "",
        "projectTotal": "",
        "projectTimeTotal": "",
        "billUnpaidTotal": "",
        "billUnpaidAmountTotal": "",
    }
}
```

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->

### Routes globales

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Obtenir un numéro pour la création d'un document

---

**Route de récupération du prochain numéro disponible pour un document.**

**URL** : `/global/nextNumber&acronym=''`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| &acronym | string | Acronyme du document pour lequel on veut récupérer le numéro (FAC, DEV, PRO, EXP, etc...) | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Successful statistic acquisition",
    "statistics": {
        "gainTotal": "",
        "expenseTotal": "",
        "employeeTotal": "",
        "customerTotal": "",
        "projectTotal": "",
        "projectTimeTotal": "",
        "billUnpaidTotal": "",
        "billUnpaidAmountTotal": "",
    }
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "114001",
    "message": "Missing important fields"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->
#### Génération d'un document

---

**Route de génération d'un document en pdf pour l'envoyer par mail.**

**URL** : `/global/generateInvoice/:type/:id`

**Methode** : `GET`

**Token requis** : `OUI`

**Paramètres de la requête**

| Paramètres | Type | Description | Obligatoire |
| ------ | ------ | ------ | ------ |
| :id | string | Id du document pour lequel | ✔️ | 
| :type | string | Précision du type de document (bill, estimate) | ✔️ | 

##### Requête réussie

**Code** : `200`

```json
{
    "error": false,
    "message": "Document successfully send"
}
```

##### Requête échouée

**Condition** : Champs obligatoires manquants.

**Code** : `400`

```json
{
    "error": true,
    "code": "114051",
    "message": "Missing important fields"
}
```

**Condition** : Format du type invalide (estimate, bill).

**Code** : `400`

```json
{
    "error": true,
    "code": "114052",
    "message": "Invalid type field"
}
```

**Condition** : Le client n'existe plus.

**Code** : `400`

```json
{
    "error": true,
    "code": "114053",
    "message": "Invalid customer id"
}
```

**Condition** : Le document n'existe pas.

**Code** : `400`

```json
{
    "error": true,
    "code": "114054",
    "message": "Invalid file id"
}
```

---

<!-- --------------------------------------------------------------------------------------------------------------------------------------------- -->

### Erreurs globales

**Condition** : Lors d'une erreur interne au serveur.

**Code** : `500`

```json
{
    "error": true,
    "message": "Unexpected error"
}
```

**Condition** : Erreur d'authentification.

**Code** : `401`

```json
{
    "error": true,
    "code": "401001",
    "message": "Not authorized to access to this resource"
}
```

**Condition** : Rôle nécessaire pour faire la requête invalide.

**Code** : `401`

```json
{
    "error": true,
    "code": "401002",
    "message": "You do not have the required permissions"
}
```
