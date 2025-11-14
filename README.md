
## Billetera Digital

Este repositorio contiene unicamente refencias de los repositorios en forma de sub-módulos de git para agilizar la descarga de los repositorios correspondientes al proyecto de Billetera Digital.

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

3. Crear un archivo .env basado en el env.example

Variables de entorno:

- BILLETERA_DIGITAL_API_PORT: Puerto en el que se ejecutará la API del proyecto (3000 default) 
- BILLETERA_DIGITAL_MS_PORT: Puerto en el que se ejecutará el microservicio del proyecto (3010 default)
- BILLETERA_DIGITAL_FRONT_PORT: Puerto en el que se ejecutará la aplicación frontend (8085 default), si se cambia hay que ajustar el puerto en el enlace de la aplicación (http://localhost:8085/)
- SMTP_HOST: Servidor de SMTP por el cual se envian los correos, por default se utiliza el servidor de google "smtp.gmail.com"
- SMTP_PORT: Puerto del Servidor SMTP 587 (TLS)
- SMTP_EMAIL: Cuenta desde la cual salen los correos "your_email@gmail.com"
- SMTP_PASSWORD: Contraseña de aplicación de la cuenta "app pass 123 123", 

La contraseña del servidor SMTP se debe generar desde la cuenta de google como Contraseña de Aplicaciones (se debe tener activado el sistema de autenticación en dos pasos)

NOTA: Solo se han hecho pruebas desde este servidor y puerto de SMTP, no se garantiza el funcionamiento para otros servidores y puertos SSL.


### Correr Proyecto

Los proyectos se pueden compilar y ejecutar usando docker usando el comando siguiente:

```
docker compose up -d
```

Una vez que se compile todo el proyecto podras acceder a la interfaz mediante el enlace de la aplicación
```
http://localhost:8085/
```

#### Tipo de dato esperado para campos de cliente

- Documento: string (UUID: df9cf233-12f0-461a-90c3-20a105afc939) 
- Nombres: string
- Email: string (correo electrónico válido)
- Celular: string (10 caracteres)


### Colección Postman

Este repositorio cuenta con archivos necesarios para importar los endpoints a Postman para hacer pruebas más rápidas, asi como las variables de entorno:

1. Billetera Digital - (Nest + Hexagonal + DDD).postman_collection.json
2. Billetera Digital.postman_environment.json

## Importante
Si se trabaja en el repositorio que tiene los sub-módulos, **primero actualizar y hacer push** en el sub-módulo y **después** en el repositorio principal. 

Si se hace al revés, se perderán las referencias de los sub-módulos en el repositorio principal y tendremos que resolver conflictos.

