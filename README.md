# **Taller de Web Scraping**

## **Parte 1: Introducción a Web Scraping**

### **Ejercicio 1: Explorar el archivo robots.txt**

1. Busca el archivo `robots.txt` de una página web y analiza sus reglas.

   - Ejemplo: [https://www.wikipedia.org/robots.txt](https://www.wikipedia.org/robots.txt)
   - Identifica qué partes están permitidas para el scraping.

2. Explicación de las reglas:
   - **User-agent**: Indica a qué rastreadores (como Googlebot o scrapers personalizados) se aplican las reglas.
   - **Disallow**: Especifica qué partes del sitio están prohibidas para el web scraping.
   - **Allow**: Especifica qué partes del sitio están permitidas para el scraping.

### **Preguntas reflexivas**

- **¿Por qué algunos sitios web bloquean el Web Scraping?**

  - El bloqueo del web scraping se da por diferentes razones, como sobrecarga del servidor, violación de los términos de servicio o uso excesivo de recursos.
  - **Sobrecarga del servidor**
    - Los robots mal diseñados pueden sobrecargar el servidor al realizar solicitudes excesivas.
  - **Violación de los términos de servicio**
    - Los sitios web pueden bloquear los raspadores web porque violan sus términos de servicio.
  - **Medidas anti-scraping**
    - Los sitios web pueden implementar CAPTCHA para diferenciar entre usuarios humanos y robots de scraping.

- **¿Cuándo es preferible usar una API en lugar de Web Scraping?**

  - El uso de una API o de web scraping depende de la necesidad de los datos, el presupuesto, los recursos tecnológicos y si el sitio web tiene una API.
  - **API**
    - Es una opción para obtener datos estructurados y confiables.
    - Permite integrar servicios de otros proveedores, como redes sociales, sistemas de pago y geolocalización.
    - Acelera el desarrollo de aplicaciones y facilita la automatización de tareas.
  - **Web Scraping**
    - Ofrece mayor flexibilidad y cobertura.
    - Permite extraer datos de sitios web que no tienen APIs.
    - Posibilita la extracción de información adicional que no está disponible en una API.

- **Herramientas populares para Web Scraping en Python**
  - La principal herramienta para el web scraping en Python es la librería `BeautifulSoup`, que facilita el análisis y extracción de datos de documentos HTML y XML.

## **Análisis del archivo robots.txt de Mercado Libre**

### **robots.txt para www.mercadolibre.com.co**

```plaintext
User-agent: Amazonbot
Disallow: /

User-agent: ClaudeBot
Disallow: /

User-agent: FacebookExternalHit
User-agent: FacebookBot
User-agent: Twitterbot
User-agent: LinkedInBot
Disallow:

User-agent: *
Disallow: /HOME/
Disallow: /gz/merch/
Disallow: /gz/menu
Disallow: /gz/webdevice/config
Disallow: /gz/referidos
Disallow: /*www.siteinfo.cf
Disallow: /gz/cart/
Disallow: /gz/checkout/
Disallow: /gz/user-logged
Disallow: /gz/shipping-selector
Disallow: /gz/navigation/searches/last
Disallow: /perfil/vendedor/
Disallow: /perfil/comprador/
Disallow: /perfil/profile/
Disallow: /perfil/jm/profile
Disallow: /perfil/ALEXSETHMS
Disallow: /noindex/
Disallow: /navigation/
Disallow: /*itemid
Disallow: /*/jm/item
Disallow: /recommendations*
Disallow: /*attributes=
Disallow: /*quantity=
Disallow: /org-img/html/
Disallow: /registration?confirmation_url*
Disallow: /home/recommendations
Disallow: /social/
Disallow: /adn/api*
Disallow: /product-fe-recommendations/recommendations*
Disallow: /*.js
Disallow: /finditem.ml
```

### **Análisis del archivo robots.txt**

1. **Bloqueo de bots específicos**

```plaintext
User-agent: Amazonbot
Disallow: /
User-agent: ClaudeBot
Disallow: /
```

- **Amazonbot** y **ClaudeBot** están bloqueados, lo que significa que no pueden rastrear ninguna parte del sitio.

2. **Bots de redes sociales permitidos**

```plaintext
User-agent: FacebookExternalHit
User-agent: FacebookBot
User-agent: Twitterbot
User-agent: LinkedInBot
Disallow:
```

3. **Restricciones generales para todos los robots**

```plaintext
User-agent: *
Disallow: /HOME/
Disallow: /gz/merch/
Disallow: /gz/menu
Disallow: /gz/webdevice/config
Disallow: /gz/referidos
Disallow: /*www.siteinfo.cf
Disallow: /gz/cart/
Disallow: /gz/checkout/
Disallow: /gz/user-logged
Disallow: /gz/shipping-selector
Disallow: /gz/navigation/searches/last
Disallow: /perfil/vendedor/
Disallow: /perfil/comprador/
Disallow: /perfil/profile/
Disallow: /perfil/jm/profile
Disallow: /perfil/ALEXSETHMS
Disallow: /noindex/
Disallow: /navigation/
Disallow: /*itemid
Disallow: /*/jm/item
Disallow: /recommendations*
Disallow: /*attributes=
Disallow: /*quantity=
Disallow: /org-img/html/
Disallow: /registration?confirmation_url*
Disallow: /home/recommendations
Disallow: /social/
Disallow: /adn/api*
Disallow: /product-fe-recommendations/recommendations*
Disallow: /*.js
Disallow: /finditem.ml
```

## **Ejercicio 2: Extracción de títulos de noticias**

```python
import requests
from bs4 import BeautifulSoup

# URL de la página de noticias
url = "https://elpais.com/tecnologia/"
headers = {"User-Agent": "Chrome/120.0.0.0"}
response = requests.get(url, headers=headers)

if response.status_code == 200:
    print(f"✅ Conexión exitosa a {url}")

# Parseamos el contenido de la página con BeautifulSoup
soup = BeautifulSoup(response.text, "html.parser")

# Extraemos los títulos con el tag h2
titulos = soup.find_all("h2")

print(f"👽 Cantidad de noticias extraídas {len(titulos)}")
for i, titulo in enumerate(titulos, start=1):
    print(f"{i}. {titulo.text.strip()}")

print(f"🤖 Extraemos las noticias que contengan algo relacionado a la IA")
i = 0
for titulo in titulos:
    if " IA " in titulo.text.upper() or "inteligencia artificial" in titulo.text.upper():
        i += 1
        print(f"{i}. {titulo.text.strip()}")
```
