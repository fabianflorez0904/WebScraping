# Taller de Web Scraping

## Introducción
En este taller, aprenderás a realizar web scraping utilizando Python y la librería `BeautifulSoup`.

## Explorar el archivo Robot.txt

Dentro del archivo `robot.txt` podemos encontrar e identificar las partes que estan permitidas y cuales, para poder realizar los procesos de WebScraping. En este formato encontramos diferentes reglas relacionadas tales que:

* **User-agent:** Indica a que rastreadores(como Googlebot o scrapers personalizados) se aplican las reglas.
* **Disallow:** Especifica que partes del sitio estan prohibidas para el web scraping.
* **Allow:** Especifica que partes del sitio estan permitidas para el scraping.

### Preguntas reflexivas
+ Por que algunos sitios bloquean el Web Scraping?
    + El bloqueo del web scraping se da por diferentes razones, como sobrecarga del servidor, violacion de los terminos de servicio, o uso excesivo de recursos.
    + **Sobrecarga del servidor**
        + Los robots mal disenados pueden provocar el servidor al realizar solicitudes excesivas.
    + **Violacion de los terminos de servicio**
