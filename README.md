# 🚀 Déploiement de Dolibarr avec Docker

## ✅ Prérequis

Avoir installé :

- Docker et Docker Compose  
- Un dossier vide pour héberger les fichiers de configuration

---

## 🛠️ Étapes détaillées

### ✅ Étape 1 : Créer un dossier de projet

Ouvre ton terminal et tape :

```bash
mkdir dolibarr-docker && cd dolibarr-docker
```

---

### 📝 Étape 2 : Créer le fichier `docker-compose.yml`

Crée un fichier `docker-compose.yml` dans ce dossier avec :

```bash
nano docker-compose.yml
```

Colle dedans le contenu suivant :

```yaml
version: "3.8"

services:
  mariadb:
    image: mariadb:latest
    container_name: dolibarr-db
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: dolibarr
    volumes:
      - db_data:/var/lib/mysql

  web:
    image: tuxgasy/dolibarr:19
    container_name: dolibarr-web
    environment:
      DOLI_DB_HOST: mariadb
      DOLI_DB_USER: root
      DOLI_DB_PASSWORD: root
      DOLI_DB_NAME: dolibarr
      DOLI_URL_ROOT: 'http://localhost:8080'
      DOLI_ADMIN_LOGIN: admin
      DOLI_ADMIN_PASSWORD: admin
      DOLI_COMPANY_NAME: BroceliandeDigital
      DOLI_COMPANY_COUNTRYCODE: FR
      DOLI_ENABLE_MODULES: Societe,Facture,Commande
      PHP_INI_DATE_TIMEZONE: 'Europe/Paris'
    ports:
      - "8080:80"
    depends_on:
      - mariadb

volumes:
  db_data:
```

💡 Tu peux adapter :

- `DOLI_ADMIN_LOGIN`
- `DOLI_ADMIN_PASSWORD`
- `DOLI_ENABLE_MODULES`

...selon tes besoins.

---

### ▶️ Étape 3 : Lancer les conteneurs

Toujours dans le dossier `dolibarr-docker`, lance la commande :

```bash
docker-compose up -d
```

Cela :

- Télécharge les images nécessaires
- Lance Dolibarr et MariaDB
- Effectue l’installation automatique

---

### 🌍 Étape 4 : Accéder à Dolibarr

Ouvre ton navigateur et va sur :

[http://localhost:8080](http://localhost:8080)

Tu devrais voir **Dolibarr prêt à l’emploi** !

---

### ✅ Tester la connexion

Va sur [http://localhost:8080](http://localhost:8080) puis connecte-toi avec :

- **Identifiant** : `admin`  
- **Mot de passe** : `admin`

---

🎉 Et voilà ! Tu as un **Dolibarr opérationnel dans Docker**.
