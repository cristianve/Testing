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


Crear una aplicación es fácil, solo hay que sentarse a codificar y ... *abemus aplication*. Tener una aplicación lista  hoy en día es algo sencillo por que si estas atascado con algo buscas en Internet y encontramos miles de ejemplos y templates que nos ayudaran a la construcción.

> *`Crear una aplicacion es fácil... pero crear una buena aplicacion lista para produccion es una historia diferente`*



Para comenzar, tenemos que estar seguros de los siguientes items:

La app es correcta ( )

- La aplicación debe ser **correcta**  (solo hace lo que debe hacer y no lo que "no debe hacer")
- La aplicación es **eficiente**  (se usa solo el tiempo asignado y no consume mas recurso de los que debería)
- La aplicación es **24/7**  (Si la aplicación solo funcionar el primer o segundo día , o todos los días hasta el fin de los tiempos).

Este ultimo punto es critico y adicionalmente necesitamos tener en mente los siguiente:

- Deberá ser facil de adaptarse al cambio 

- Deberá ser fácil realizar mejoras

- Deberá ser fácil de expandirse

  

Crear una aplicación es fácil y (en principio) muy rápido. La creación de una aplicación excelente, lista para producción requiere un pensamiento cuidadoso, planificación e ingeniería. Sí, también puedes optar por la filosofía *'Déjalo crecer con el tiempo'*; La naturaleza tiene millones de ejemplos en los que esto funciona perfectamente bien. La cuestión es, que lleva a la naturaleza millones de años, y es posible que no estés dispuesto a esperar tanto.

Hoy en día unos de los problemas mas comunes es que creamos una aplicación en base al modelo de datos dejando de pensar en el core del negocio.

Y luego se pretende que esa aplicación evolucione fácilmente como nuestro negocio :( esto ya pasa a ser una tarea compleja por que indistintamente sabemos que estamos limitados a las relaciones de nuestro modelo de persistencia en caso de ser SQL.

Otro enfoque que a veces nos aterra al vernos es cuando se construyen aplicaciones del tipo BFF (backend for frontend). Donde nuestros microservicios pasan de ser apis restful  ser agregadores de modelos.

Con el fin de evitar estos sucesos vamos a explicar los siguientes conceptos.



# Components

Fred Brooks “[*No Silver Bullet*](http://faculty.salisbury.edu/~xswang/Research/Papers/SERelated/no-silver-bullet.pdf)” lo describe de una manera excelente. El desarrollo de aplicaciones tiene problemas al relacionar la "esencia" del dominio, y esto deriva en decisiones  (el "accidente").


Model Entities y el Use Case son componentes que en su conjunto se llaman **core**. 

Este dominio tiene el conocimiento y lo que se quiere implementar a futuro.

El *accidente* esta compuesto por lo siguiente:

- Delivery

- Gateway

- Repository

- External Libraries

- Configuration

- Main


El desarrollo no siempre es perfecto,  necesitamos mucho soporte de la "essence" para que esto funcione en un entorno real. Estos componentes lo conocemos como **Infraestructure**

## Model entities

![img](https://miro.medium.com/max/60/1*HOUiqrWI4xqZuwJei4jkbg.png?q=20)

![](C:\Users\juanlope\Documents\CleanArquitecture\cleanmodel.png)

![Cleanarqutiectrodiagram](C:\Users\juanlope\Desktop\Cleanarqutiectrodiagram.png)

# Core

## Components

> Entidades encapsuladas donde  Enterprise wide business rules.

El core se describirá como la Entidad, como el Model y el Caso de uso. Estos términos están relacionados con el ***core***, en otras palabras, aquí esta representado el dominio y las "features (ports)" que queremos implementar.

El accidente esta compuesto por el resto: Delivery, Port Implemntation, Repository, Library support, configuration y main. Todo esto es necesario para que nuestro **core** funcione, ya que en la vida real se  necesita el soporte de frameworks. A estos componentes lo llamamos **"*infraestructura*"**

## Use cases

> Los casos de uso tienen reglas de negocio especificas de la aplicación

Encpsula e implementa todos los casos de uso del sistemas. Estos casos de uso organizan los flujos de datos hacia y desde las entidades. Ademas controla que esas entidades usen sus reglas de negocio para toda la aplicación, para lograr los objetivos del caso de uso.



# Infraestructure

Quien nos dara el soporte para que nuestra aplicacion funcione sera este section



### Delivery

> *En la delivery, encontramos los adaptadores de interfaz, que reciben solicitudes desde el exterior del microservicio y entregan (de ahí su nombre :-)).*

Es común implementarlo como un servicio http rest, o consumir mensajes de algún intermediario de mensajes (como cualquier servidor JMS, RabbitMQ, etc.). 



### Gateways

> *Las puertas de enlace son adaptadores de interfaz que permiten que este microservicio solicite servicios a otros microservicios (legay or external services).*

Es común ver implementaciones como llamadas http, clientes de message borker o cualquier otro cliente API.



### Repositories

> Estos adaptadores son destinados a almacenar y recuperar objetos de una aplicación (serializados), mayormente estos representan una entidad.

La diferencia entre los repositorios y los gateway es que los gateway usualmente son utilizados para comunicarse con otros sistemas, pero (en la arquitectura de microservicio) el datastore solo debe ser utilizado por este servicio. Esto pertenece al limite lógico del Bounded context ( Domain driven desing).



### Configuration



> La configuración es la parte de la aplicacion que define los comportamientos los diferentes componentes para que una aplicación se ejecute.

Contiene las factories de los los componentes y realiza una inyección de dependencia para vincular los diferentes componentes de tal manera que en este modulo creamos nuestra aplicacion segun las implmentaciones que vallamos realizando.

También tiene la lógica para recopilar datos de configuración de parámetros de aplicación, variables de entorno o archivos de configuración externos que se utilizan en el proceso de creación para permitir que este conjunto se " *parametrice* ".

### Main

Su propósito es llamar a la configuración y darle *run* a la aplicación.

Alguien lo tenia que hacer :)



# Process flow

Para que estas palabras anteriores tengan sentido es necesario que los componentes interactuen entre ellos de la siguiente manera. Realizando es siguiente patrón de comportamiento

![img](https://miro.medium.com/max/60/1*t7IMWNKcNwnoBHgQzQor1A.png?q=20)

![img](C:\Users\juanlope\Documents\CleanArquitecture\cleancircuit.png)

**Request Process Flow**

1. Un **sistema externo** realiza una solicitud (una solicitud HTTP, un mensaje JMS está disponible, etc.).

2. El **delivery** crea varias entidades modelo a partir de los datos de la solicitud.

3. El **delivery** llama a una acción de caso de uso (comando, interacción, etc.)

4. El **usecase** opera en entidades modelo.

5. El **usecase** hace una solicitud para leer / escribir en el repositorio.

6. El **repository** consume alguna entidad modelo de la solicitud de caso de uso.

7. El **repository** interactúa con la persistencia externa (comando DB, comando del sistema de archivos).

8. El **repository** crea entidades modelo a partir de los datos persistentes.

9. El **usecase** solicita colaboración de una puerta de enlace.

10.    El **gateway** consume las entidades modelo proporcionadas por la solicitud de caso de uso.

11.    La **gateway** interactúa con servicios externos (otras aplicaciones, coloca mensajes en colas, imprime en una impresora, etc.).

​    

# Dependencies

En base al diagrama anterior el siguiente diagrama marca un poco las "dependencia entre las capas"

![img](https://miro.medium.com/max/60/1*iIiSmy0wRvVW-Wuaj_0tkg.png?q=20)

![img](C:\Users\juanlope\Documents\CleanArquitecture\clean-dependencies.png)

En la imagen, las secciones más oscuras están relacionadas con procesos más detallados y más específicos de la tecnología (*accidente*), mientras que las más claras son más conceptuales (*Esencia*).

En detalle:

- Todo depende de las Entidades del Modelo de Negocio, que deberían ser los elementos más estables y los más importantes.
- El delivery, el repository y los gateway (la capa de infraestructura en clean arquitecture y otros modelos) dependen de los use case (las reglas de negocio de la aplicación) y las entidades modelo *(1)*. Estos dos últimos son el núcleo del negocio.

Todos los componentes pueden depender de bibliotecas compatibles:

- Las entidades modelo requieren un frameworks para tener listas, conjuntos, etc. Además, podrían necesitar un soporte de fecha y hora, algunas matemáticas, etc.
- Los use case necesitan soporte para el procesamiento de colecciones, la lógica empresarial específica, la gestión de concurrencia (sí, no siempre se puede configurar de forma transparente) y otros
- El delivery necesita soporte del servidor HTTP, JSON u otras conversiones, validaciones JWT, etc.
- Los gateway requieren clientes HTTP, clientes del servidor de cola, etc.
- Los repository requieren clientes DB

*(1)* Muchos argumentan que las entidades modelo no deberían ser visibles desde la infraestructura. No estoy completamente convencido de que ganamos y que la separación valga la mayor complejidad cuando se trata de microservicios (no deberíamos tener 200 clases). 



# Java Implementation



# Model entities

Las entidades modelo son clases de datos simples de Java (no sé si alguien acuñó el término fin, pero POJO tiene más estilo y apariencia de marketing).



```java
@Data
@AllArgsConstructor
public final class Category implements Serializable {

	private static final long serialVersionUID = -5611389089964568317L;

	private Long id;

	private String name;

	private Boolean available;
	
}
```

# Use cases

Los casos de usos se implementan mediante un conjunto de acciones donde toda la logica de nogocio es es implementada aqui se realizara el tratamiento de nuestros objetos de dominio asi como la tambien las llamadas a nuestros repositorios y gateways.



Ejemplo de una accion simple:

```java
@AllArgsConstructor
public class GetAllCategoriesUseCaseImpl implements GetAllCategoriesUseCase {

	private final CategoryRepositoryService categoryRepositoryService;

	@Override
	public Collection<Category> execute() {
		return categoryRepositoryService.getAllCategories();
	}

}
```

Este caso de uso es simple solo importa el repositorio para traer todas las categorías persistentes, pero de ser necesario puedo implmentar otros gateway o repositories , todo lo que sea necesario para complementar mi modelo o ejecutar mi accion.



# Delivery

El delivery consta de un grupo de controladores (handlers) . Cada controlador maneja solicitudes específicas, convierte el peyload a DTO o entidades modelo, y llama a la acción apropiada. Finalmente, convierte la respuesta de user en la carga útil de respuesta y la devuelve a la persona que llama.



```java
@RestController
@RequestMapping(RestConstants.APPLICATION_NAME + RestConstants.API_VERSION_1 + RestConstants.RESOURCE_CATEGORY)
@RequiredArgsConstructor
public class CategoryControllerImpl implements CategoryController {

	private final GetAllCategoriesUseCase getAllCategoriesUseCase;
	private final CreateCategoryUseCase createCategoryUseCase;
	private final CategoryRestConverter categoryRestConverter;

	@Override
	@ResponseStatus(HttpStatus.OK)
	@GetMapping(produces = MediaType.APPLICATION_JSON_VALUE)
	public NetflixResponse<Collection<CategoryRest>> getCategories() throws NetflixException {
		return new NetflixResponse<>(CommonConstants.SUCCESS, 				  								String.valueOf(HttpStatus.OK), CommonConstants.OK,
					getAllCategoriesUseCase.execute().stream()
                    .map(category -> categoryRestConverter.mapToRest(category))
					.collect(Collectors.toList()));
	}
    
....
    
public class CategoryRestConverter implements RestConverter<CategoryRest, Category> {

	@Override
	public Category mapToEntity(final CategoryRest rest) {

		return new Category(null, rest.getName(), rest.getAvailable());
	}

	@Override
	public CategoryRest mapToRest(final Category entity) {
		return new CategoryRest(entity.getName(), entity.getAvailable());
	}

}
......
    
  
```

El controlador no tiene lógica más allá de la transformación (serialización, deserialización) y la llamada a la acción. Toda la lógica de negocios debería estar detrás del user case.

# Gateways

```java
@FeignClient(name="filmClient", url= "http://storage-image/film-info/film/") 
public interface StorageImageRestClient{

    @RequestMapping(method = RequestMethod.GET, value = "{id}", produces = "application/json")
    StoraImage findById(@PathVariable("id")final Long id);

}
```

Aquí el Gateway aprovecha un FeignClient provisto para conectarse a un servicio externo.

Una vez más, el Gateway no tiene lógica de negocios, sino conversiones y mapeos

# Repositories

En la persistencia se implementa los repositorio propios de JPA o los customs ademas de inyectar los converter 

```java
@AllArgsConstructor
public class CategoryPersistenceImpl implements CategoryRepositoryService {

	private CategoryRepository categoryRepository;
	private CategoryRepositoryConverter categoryRepositoryConverter;

	@Override
	public Collection<Category> getAllCategories() {
		return categoryRepository.findAll().stream().map(category -> categoryRepositoryConverter.mapToEntity(category))
				.collect(Collectors.toList());
	}

	@Override
	public void saveCategory(Category category) throws NetflixException {
		if (doesCategoryNameExists(category.getName()))
			throw new BadRequestException(ExceptionConstants.BAD_REQUEST_EXISTS_CATEGORY_MESSAGE);
		categoryRepository.save(categoryRepositoryConverter.mapToTable(category));
	}

	private Boolean doesCategoryNameExists(String name) {
		return !categoryRepository.findByName(name).isEmpty();
	}

}

```



# Configuration

Aqui configuraremos el comportameinto de nuestros persistence de nuestros deliverys y sobre todo nuestros casos de uso, si queremos que algunos de nuestros componentes o capaz tengan un comportamiento diferente es tan simple como implementar otra comportamiento de nuestro bean

```java
@Configuration
public class CategoryConfiguration {

	@Autowired
	private CategoryRepository categoryRepository;


	@Bean
	public CategoryRepositoryConverter createCategoryRepositoryConverter() {
		return new CategoryRepositoryConverter();
	}

	@Bean
	public CategoryRestConverter createCategoryRestConverter() {
		return new CategoryRestConverter();
	}

	@Bean
	public CategoryServiceImpl createCategoriServiceImpl() {
		return new CategoryServiceImpl(categoryRepository, createCategoryRepositoryConverter());
	}

	@Bean
	public GetAllCategoriesUseCaseImpl createGetAllCategoriesUseCase() {
		return new GetAllCategoriesUseCaseImpl(createCategoriServiceImpl());
	}
	
	@Bean
	public CreateCategoryUseCaseImpl createCreateCategoryUseCase() {
		return new CreateCategoryUseCaseImpl(createCategoriServiceImpl());
	}

}
```



# Main

La clase mas aburrida:

```java
@SpringBootApplication
public class Application {

	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}

}
```



# **Conclusiones**



Crear grandes aplicaciones es un desafío, pero una buena estructura y el seguimiento correcto de algunos principios pueden ayudar mucho en su desarrollo. La arquitectura mostrada nos permite crear aplicaciones que son fáciles de entender, fáciles de cambiar y fáciles de solucionar. La separación correcta de las capas nos proporciona una base sólida.

Puede que el enfoque a un principio sea chocante al desarrollo por capas, pero lo importante es que este articulo sirva como guia y no como limitante, comenzar a desarrollar con esta arquitectura puede que cueste un poco mas de esfuerzo a un principio pero luego la evolucion del mismo es mas facil de aplicar, asi mismo de entender.

Como dicen clean arquitecture es una serie de reglas y principios:

- SOLID
- DRY
- SRP
- KISS
- Clean Code :)

que si lo aplicamos de una manera coherente nuestro proyecto sera clean.





