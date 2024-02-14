# Hur gör man en Deploy

- [Link to English version](README(EN).md)

### Man ska börja med att skapa konton på Vercel och Aiven

- [Länk till Vercel](https://vercel.com/login)
- [Länk till Aiven](https://aiven.io)

### Vercel

**Tryck på sign up uppe i högra hörnet**

<img src="./images/image-2.png" alt="Vercel Sign Up">
<br>

**Välj hobby och skriv in ditt namn sedan continue**

<img src="./images/image-4.png" width=350 alt="Vercel Create Account">
<br>

**Fortsätt sedan med GitHub**

<img src="./images/image-1.png" height=300 alt="Vercel Login">
<br>

**Nu måste man se till att man har ett GitHub repo som man är redo att deploy**
- Först måste du igen ge tillgång till din GitHub.
- När du har en repo och har gett tillgång ska du importa det repot som du vill deploy.
- Nu dags att gå vidare till *Aiven*.


### Aiven

**Tryck på Get started for free uppe i högra hörnet**

<img src="./images/image.png" alt="Aiven Start">
<br>

**Här kan vi också fortsätta med GitHub**

<img src="./images/image-5.png" alt="Aiven Create account">
<br>

**Sen vill vi välja MySQL**

<img src="./images/image-6.png" alt="Aiven MySQL">
<br>

**Sen vill vi välja en Free plan**

<img src="./images/image-7.png" alt="Aiven Free">
<br>

**Nu har vi fått all information för att kunna logga in till databasen med adminer**

<img src="./images/image-8.png" alt="Aiven db info">
<br>


### Sista steget innan Deployment

- Först vill vi skapa en mapp i rootmappen som heter **api**. I den mappen vill vi skapa en fil som heter **"index.php"** där vi ska skriva in en kod. Den koden är till för att Vercel ska veta vart applikationen ligger i projektet. **Code:**
```ruby
<?php
// Forward Vercel requests to normal index.php
require __DIR__ . '/../public/index.php';
```
- Sedan vill vi skapa en fil i rootmappen som heter **"vercel.json"**. I den ska vi också lägga in en del kod som är till för att configurera projektet för deployment via Vercel.
**Code:** 

```ruby
{
    "version": 2,
    "framework": null,
    "functions": {
    "api/index.php": { "runtime": "vercel-php@0.6.1" }
    },
    "routes": [{
    "src": "/(.*)",
    "dest": "/api/index.php"
    }],
    "env": {
    "APP_ENV": "production",
    "APP_DEBUG": "true",
    "APP_URL": "https://yourproductionurl.com",
    "APP_CONFIG_CACHE": "/tmp/config.php",
    "APP_EVENTS_CACHE": "/tmp/events.php",
    "APP_PACKAGES_CACHE": "/tmp/packages.php",
    "APP_ROUTES_CACHE": "/tmp/routes.php",
    "APP_SERVICES_CACHE": "/tmp/services.php",
    "VIEW_COMPILED_PATH": "/tmp",
    "CACHE_DRIVER": "array",
    "LOG_CHANNEL": "stderr",
    "SESSION_DRIVER": "cookie"
    }
}
```
- Nu är det ett sista steg vilket är att databas informationen man fick i Aiven ska då läggas in i .env filen i ditt projekt. Så kollar man i Aiven så fick vi Host, Port, User, Password de ska då sättas in i denna del av .env filen.

```ruby
DB_CONNECTION=mysql
DB_HOST= "Host"
DB_PORT= "Port"
DB_DATABASE= 
DB_USERNAME= "User"
DB_PASSWORD= "Password"
```

### Deployment

**Nu är det absolut sista steget**
Vilket då är att pusha till ditt repo och sedan gå in i Vercel och trycka på deploy. 


**Nu har du deployed ditt projekt!**