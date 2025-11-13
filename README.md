
## Billetera Digital

Este repositorio contiene unicamente refencias de los repositorios en forma de submodulos de git para agilizar la descarga de los repositorios correspondientes al proyecto de Billetera Digital.

## Tabla de Contenido

---

- [Estructura de Proyecto](#estructura)
- [Ejecutar Proyecto](#como-ejecutar-el-proyecto)

---

### Estructura

#### Microservicio Billetera Digital (billetera-digital-ms)

Contiene la lógica de negocio del proyecto, en el cual se implementa una combinación de arquitecturas como Screaming (Modulos) + Hexagonal (Capas de aplicación, dominio e infraestructura).

Asi mismo se busco aplicar de la mejor forma la metodologia DDD (Domain Driven Design), aunque no es apto para todos los proyectos (en especial para proyectos pequeños) decidí utilizarlo para llevarlo a la práctica ya que en cada oportunidad busco poder implementar algo nuevo y no quedarme encerrado en lo de siempre.

Este proyecto contará con 3 módulos:

1. Clientes (Completo)
2. Billetera (Completo)
3. Pagos (Pendiente)

Estos módulos implementando arquitectura hexagonal y DDD pretende evaluar e implementar la lógica de negocio, una vez evaluada se almacena la información en la base de datos (MongoDB).

#### API Billetera Digital (billetera-digital-api)

Este proyecto funciona como puerta de enlace hacia el microservicio de billetera digital, no contiene logica de negocio unicamente tiene la infraestructura para recibir peticiones HTTP por parte de un cliente y mediante un Broker de mensajeria (Servidor de NATS en este caso) envia los mensajes al microservicio para obtener una respuesta y regresarla al cliente.


#### Front Billetera Digital (billetera-digital-front)

Se desarrollo una aplicación sencilla como cliente para realizar las peticiones correspondientes a la API de billetera digital usando la librería de React.

Decidí usar React debido a que es una área de mejora en cuanto a desarrollo de aplicaciones Front-End, ya que mi mayor expertis se inclina hacia Vue 3, pretendo mejorar en el uso de React.

## Como ejecutar el proyecto

### Docker

Para una ejecución simple y rápida se recomienda instalar [Docker](https://www.docker.com/).

### Clonar Proyectos

Se pueden clonar los proyectos rápidamente en 2 pasos:

1. Clonar este repositorio en la maquina local:
```
git clone https://github.com/RojoRandy/billetera-digital-launcher.git
```

2. Inicializar y actualizar Sub-módulos, cuando alguien clona el repositorio por primera vez, debe de ejecutar el siguiente comando para inicializar y actualizar los sub-módulos

```
git submodule update --init --recursive
```

### Correr Proyecto

Los proyectos se pueden compilar y ejecutar usando docker usando el comando siguiente:

```
docker compose up -d
```


## Importante
Si se trabaja en el repositorio que tiene los sub-módulos, **primero actualizar y hacer push** en el sub-módulo y **después** en el repositorio principal. 

Si se hace al revés, se perderán las referencias de los sub-módulos en el repositorio principal y tendremos que resolver conflictos.

