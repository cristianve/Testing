# Pensando Apimente – Builids APIs
# D4I Team– everis

## Contenido  

* 1. ¿Por donde comienzo?
  * 1.1. Nomenclatura: URLs, E/S e ISOs
  * 1.2. Tipología de recursos
* 2. ¿Cómo interaccionar con métodos HTTP?
  * 2.1. Uso de verbos HTTP
  * 2.2. ¿Cómo responder de manera correcta?
  * 2.3. ¿Cómo versiono?
  * 2.4. ¿Cómo pagino?
  * 2.5. ¿Cómo filtro los resultados?
  * 2.6. ¿Cómo ordeno los resultados?
* 3. Metodología de diseño de recursos
* 4. Ejemplo

## 1. ¿Por donde comienzo? 🤔🎬

# Api product 📦

Los API son productos que se ofrecen en un mercado (API Portal) para cubrir una necesidad de un grupo de clientes (Consumidores de APIs) 
Esto no se interpreta para satisfacer las necesidades de una sola persona o un caso único, sino pensar en la funcionalidad genérica para un grupo que consume aplicaciones y soluciones 

# Api First 1️⃣

Ventajas de diseñar APIs antes de realizar una implementación del servicio:
* Mejor entendimiento el negocio
* Menos iteraciones y cambios posteriores
* Cambios en diseños menos complejos, fáciles y rápidos


# Definir guía de diseño

* Conseguir que las APIs tengan la misma morfología independientemente del equipo/proyecto que las diseñe e implemente.
* Facilitar el uso por parte del consumidor  evitando heterogeneidad  por ejemplo de respuesta de error, códigos HTTP, etc.
* Ayudar a los proyectos en la toma de decisión de diseño de los recursos para conseguir APIs agnósticas del proyecto, que se puedan reutilizar y sean funcionales.

## 1.1 Nomenclatura

![IMAGE MAIN 1](/images/foto1.PNG)