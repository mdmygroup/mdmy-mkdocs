# 📘 APIs

---

## 🧩 Qu’est-ce qu’une API ?

**API** est l’acronyme de **"Application Programming Interface"**, ou **interface de programmation d’application** en français.

C’est une **passerelle** qui permet à deux logiciels différents de **communiquer entre eux**. Une API définit **un langage commun** que ces logiciels peuvent utiliser pour **échanger des données ou des instructions**.

> 💡 **Métaphore simple :** Imaginez une API comme **le serveur dans un restaurant**. Vous (le client) commandez via le menu (l’interface), le serveur (l’API) transmet la commande au chef (le logiciel ou système en arrière-plan), puis vous apporte votre plat.

---

## ⚙️ Comment fonctionne une API ?

Une API fonctionne selon un principe simple : **elle reçoit une requête, traite cette requête, puis renvoie une réponse**.

Voici les étapes clés :

1. **Le client envoie une requête** à l’API (par exemple : “donne-moi les horaires des trains”).
2. **L’API transmet cette demande** au système ou à la base de données concernée.
3. **Le système exécute l’action** (ex. : récupère les horaires depuis une base de données).
4. **L’API renvoie la réponse** au client (les horaires des trains sont affichés).

> 📌 Les requêtes et réponses sont souvent échangées en **format JSON**, un format de données simple et lisible.

---

## 🔁 Exemple concret d’API dans la vie quotidienne

### 🌐 Utiliser une application météo

Quand vous ouvrez une application météo :

- Elle **envoie une requête** à une API météo (comme celle de Météo France ou OpenWeather).
- Cette API **récupère les données** météo actuelles de votre ville.
- Puis elle **les renvoie à votre application**, qui vous les affiche joliment.

---

## ✅ Pourquoi utilise-t-on autant les APIs ?

Les APIs sont partout car elles permettent de :

| Avantage | Explication |
|---------|-------------|
| 🔌 **Connecter facilement** | Permettre à différentes applications de fonctionner ensemble. |
| ♻️ **Réutiliser le code** | Un service peut être utilisé par plusieurs applications (ex : une API de paiement utilisée par plusieurs sites e-commerce). |
| 📦 **Modulariser** | Créer des systèmes flexibles composés de briques réutilisables. |
| 🔒 **Sécuriser l’accès** | L'API peut filtrer et contrôler l’accès aux données sensibles. |

---

# 🤖 Et les LLMs dans tout ça ? Introduction aux **MCP Servers**

---

## 🔍 Qu’est-ce qu’un MCP Server (Model Context Protocol) ?

Dans le contexte de l’intelligence artificielle et des **grands modèles de langage** (LLM, comme ChatGPT), un **MCP Server** est un **serveur qui gère l’environnement dans lequel le modèle opère**.

- Il **fournit le contexte** : les règles, les connaissances, les outils à disposition du modèle.
- Il **structure les échanges** entre l’utilisateur, le modèle et d’autres systèmes (bases de données, API externes, outils métier, etc.).
- Il **oriente les réponses** du modèle en fonction de sa configuration (ex. : modèle expert médical, juridique, etc.).

---

## 🔄 Quel lien avec les APIs ?

Les MCP Servers **exposent souvent une ou plusieurs APIs** que les LLMs utilisent pour :

- **Récupérer des données en temps réel** (via des API météo, financières, internes à l’entreprise…).
- **Déclencher des actions** (comme envoyer un email, créer un ticket, interagir avec un CRM).
- **S’intégrer à des systèmes externes** de manière fluide et dynamique.

> 🧠 Exemple : Un modèle GPT configuré pour la gestion RH peut interroger une API interne d’entreprise via un MCP Server pour connaître les congés disponibles d’un collaborateur.

---

## 🧱 Synthèse

| Élément | Rôle |
|--------|------|
| **API** | Sert de pont entre deux systèmes, pour échanger des données ou exécuter des actions. |
| **LLM (modèle)** | Génère du texte ou des réponses à partir de données et d’instructions. |
| **MCP Server** | Organise l’environnement du modèle, expose des API, orchestre les interactions. |

---

## 🧩 Conclusion

Les **APIs sont des fondations invisibles mais essentielles** du numérique moderne. Elles permettent aux services, logiciels et maintenant aux intelligences artificielles comme les LLMs de **travailler ensemble**.

Les **MCP Servers**, dans le cadre des LLMs, représentent une **nouvelle couche d’orchestration intelligente**, souvent pilotée **via des APIs** : ce sont des “cervelles organisationnelles” qui dirigent les modèles pour leur faire accomplir des tâches concrètes.
