# Accueil

## Présentation

Bienvenue sur le centre de documentation officiel de MDMY GROUP. Ce site contient des guides complets, des références et des ressources pour vous aider à tirer le meilleur parti de nos services dans le domaine du développement web et des stratégies digitales.

## Caractéristiques

- **Navigation Intuitive** : Parcourez notre documentation à l'aide du menu de navigation à gauche.
- **Recherche Efficace** : Trouvez des informations spécifiques grâce à la fonction de recherche en haut de page.
- **Compatible Mobile** : Accédez à la documentation en déplacement depuis votre appareil mobile.
- **Imprimable** : Imprimez n'importe quelle page ou section pour une consultation hors ligne.

## Notre Mission

Chez MDMY GROUP, notre mission est d'accompagner les TPE, PME et artisans français dans la création et le développement de leur présence digitale. Nous créons des sites web sur-mesure et des applications web innovantes, tout en concevant des stratégies digitales complètes pour aider nos clients à maximiser leur visibilité et leur impact en ligne.

## Sections de Documentation

| Section | Description |
| ------- | ----------- |
| [Documentation Générale](documentation-generale/introduction.md) | Introduction et guide de la charte graphique |
| [Guides Techniques](guides-techniques/index.md) | Guides techniques détaillés pour les API, GitHub, Icon8, et Shopify |

## Support

Si vous avez besoin d'aide au-delà de ce qui est couvert dans notre documentation :

- Contactez notre support à [contact@mdmygroup.com](mailto:contact@mdmygroup.com)
- Appelez-nous au +33 6 99 41 05 87
- Visitez notre site web [www.mdmygroup.com](https://www.mdmygroup.com)

## 📚 Documentation Disponible

{% for section in navigation %}
  {% if section.is_section %}
### {{ section.title }}

    {% for child in section.children %}
      {% if child.is_section %}
#### {{ child.title }}

        {% for page in child.children %}
          {% if page.is_page and not page.url.endswith("index.html") %}
- [{{ page.title or page.url.split('/')[-2]|replace('-', ' ')|capitalize }}]({{ page.url }})
          {% endif %}
        {% endfor %}

      {% elif child.is_page and not child.url.endswith("index.html") %}
- [{{ child.title or child.url.split('/')[-2]|replace('-', ' ')|capitalize }}]({{ child.url }})
      {% endif %}
    {% endfor %}

  {% elif section.is_page and not section.url.endswith("index.html") %}
- [{{ section.title or section.url.split('/')[-2]|replace('-', ' ')|capitalize }}]({{ section.url }})
  {% endif %}
{% endfor %}


---

*Dernière mise à jour : Mai 2025*