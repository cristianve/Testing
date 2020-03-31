# Pensando Apimente – Builids APIs 🎓🏭
# D4I Team– everis

## Contenido 📇

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


# Definir guía de diseño 📖

* Conseguir que las APIs tengan la misma morfología independientemente del equipo/proyecto que las diseñe e implemente.
* Facilitar el uso por parte del consumidor  evitando heterogeneidad  por ejemplo de respuesta de error, códigos HTTP, etc.
* Ayudar a los proyectos en la toma de decisión de diseño de los recursos para conseguir APIs agnósticas del proyecto, que se puedan reutilizar y sean funcionales.

## 1.1 Nomenclatura ✏️🔤


![IMAGE MAIN 1](/images/foto1.PNG)

* Anatomía de una URL

* Nombre de los recursos

* Path parameters

* Query parameters

* Campos de entrada/salida


## 1.2 Tipos de recursos 🤔🎬

### ¿Qué es un recurso?

* Un Recurso representa una Entidad del mundo Real, como por ejemplo:  Persona, Pago, Factura…
* Es la información a la que queremos acceder o que queremos modificar o borrar, independientemente de su formato.
* Pueden ser accedidos utilizando un identificador global.
* Los componentes de la red (clientes y servidores) se comunican a través de una interfaz estándar (HTTP) e intercambian representaciones de estos recursos


## 2. ¿Cómo interaccionar con los métodos HTTP? ↔️

## 2.1. Uso de métodos HTTP

* *GET*
* *POST*
* *PUT*
* *PATCH*
* *DELETE*


## 2.2. ¿Cómo responder adecuadamente?

### Formatos acceptables 📰 

### Los codigos HTTP ⛔⚠   

* 1XX Respuestas informativas

* 2XX Peticiones correctas

* 3XX Redirecciones

* 4XX Errores del cliente

* 5XX Errores del servidor

### Formato de respuesta común  ↩

## 2.3 ¿Cómo versiono? 💾

**Técnicas de versionado:**
 
* Versionado en la URL de la invocación

* Versionado en la definición de la API:  Configurando el versionado de Swagger.

* Versionado en la URL de la invocación



## 2.4 ¿Cómo paginar? 📄

**Técnicas de paginación:**

* Paginación con offset

* Paginación basada en tiempo

* Paginación basada en cursor o identificador


**Propuesta de paginación**

* Petición

* Respuesta

## 2.5 ¿Cómo filtrar los resultados? 🔍

* **Filtrado básico:** Ventajas, buenas prácticas y ejemplos de filtrado.


## 2.6 ¿Cómo ordenar resultados de un recurso? 🔢🔠

* **Técnicas de ordenación:** Explicación de las diferentes tecnicas , filtrado y buenas prácticas.

## 3. Metodología de diseño de recursos ✍️🗺️

![IMAGE MAIN 3](/images/foto3.PNG)

## 4. Netflix Ejemplo 📺

### Disseño de una API funcional basandonos en el ejemplo de la plataforma Netflix:

![IMAGE MAIN 3](/images/foto4.PNG)
