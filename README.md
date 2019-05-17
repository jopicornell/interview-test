# Descripción
Básicamente el proyecto consistirá en una aplicación para gestionar pedidos de una tienda de informática. Podremos crear un pedido y ver el detalle de pedidos existentes, así cómo una lista de usuarios. El objetivo de este proyecto es ver cómo te desenvuelves al crear módulos, formularios y algo de estilo. No hace falta que corras, si ves que se te echa el tiempo encima, céntrate sólo en una pantalla (preferiblemente el formulario de creación del pedido). No porque sólo hagas una parte será peor; si haces una pero bien, mejor que hacer todo, pero mal. Tómate tu tiempo y **Pideme todo lo que quieras**, aunque creas absurdo. Tampoco será negativo que me preguntes cómo hacer las cosas o ayuda ante errores. 

Durante toda la documentación encontrarás links de interés, por si no te acuerdas de algo ;)

# Encender la aplicación
Para que todo funcione correctamente, deberás ejecutar `npm start` (para ejecutar Angular) y `npm server` (para ejecutar el servidor de datos) en dos consolas diferentes.

# Tecnologías
Ya te hemos hecho el proyecto para que puedas usar [Angular Material](https://angular.material.io) libremente. Se te pedirá que uses componentes de esta librería y se te indicará en esta documentación el link al componente directamente. Puedes instalar otras librerías cómo Bootstrap, en eso no hay limitación. Lo que te sientas más cómodo. También hemos instalado [ngx-toastr](https://www.npmjs.com/package/ngx-toastr) para que puedas mostrar mensajes al usuario. 

Hemos utilizado un servidor mockeado para que puedas hacer peticiones a él y recibir datos. Dicho servidor se ejecuta con `npm start` y podrás acceder a él con la url http://localhost:8080.

# La aplicación
La aplicación en sí consistirá en [dos módulos](https://angular.io/guide/architecture-modules): Pedidos y usuarios. Lo principal son los pedidos (_/src/offers_), así que cuida los detalles en este módulo. El módulo de usuarios sólo sirve para mostrar y buscar usuarios. 

## Pedidos
### Service
Deberás crear un service para gestionar todas las llamadas a la api. Deberás usar RxJS y Observables, algo no muy dificil ya que [HttpClient](https://angular.io/guide/http) ya los utiliza. Para los pedidos seguramente necesitarás métodos para crear (POST `http://localhost:8080/orders`), listar (GET `http://localhost:8080/orders`) y ver el detalle (GET `http://localhost:8080/orders/{id}`). 
### Lista de pedidos
La lista de pedidos se realizará con [MatTable](https://material.angular.io/components/table/overview), y tendrá las siguientes columnas: Código (code), Fecha (date), Usuario (user.name + user.lastName) y Total (total). La columna fecha tendrá formato dd/mm/YYYY y la de precio "123,90 €". Al hacer click en alguna fila, directamente te llevará al detalle del pedido. Debido a las limitaciones del mock server sólo estará disponible el pedido número 1, pero esto lo aprovecharemos para capturar el error y mostrar un toaster de error cuando esto suceda (tienes un ejemplo de toaster en _app/app.component.ts_). En la pantalla deberá aparecer un botón para crear un nuevo pedido (y te llevará a la creación del pedido).
### Detalle de pedido
El detalle del pedido contendrá toda la información del pedido: Código, Fecha, Usuario, todos los items y, al final, el total. Se deberá poder volver atrás para ver la lista de pedidos otra vez.
### Creación de un pedido
Para la creación de un pedido deberás usar [Reactive forms](https://angular.io/guide/reactive-forms). El usuario deberá poder seleccionar el usuario de un dropdown (disponible desde el Service de usuarios), elegir la fecha con un [datepicker](https://material.angular.io/components/datepicker/overview) y añadir artículos. Para añadir artículos se utilizará un botón que abrirá un [MatDialog](https://material.angular.io/components/dialog/overview) que pedirá el artículo, la cantidad y el total. Al darle a aceptar, se añadirá una línea y se calculará el total. El total será un texto siguiendo el formato "132,45 €".

## Usuarios
### Service
Deberás crear un service para gestionar la lista de usuarios (GET `http://localhost:8080/users`).
### Lista de usuarios
La lista de usuarios se realizará con [MatTable](https://material.angular.io/components/table/overview). En la parte superior aparecerá un campo de búsqueda dónde se podrá buscar por nombre y apellidos. La búsqueda se realizará mientras se va escribiendo. La búsqueda se realizará con Angular.
