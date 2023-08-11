# Nucba Zappi 🍕

## Descripción y objetivos

En este repositorio encontrarán un proyecto simple de Front-End realizado con React con el cual realizaremos la integración con nuestra API de Nucba Zappi.
El principal objetivo de esta app es tener un Front mediante el cual podamos interactuar con la API que realizamos en el módulo de Backend desde un entorno que no sea Postman.

Importante: Nos parece importante recordar que algunos alumnos solo se anotan para realizar el módulo de Backend. Con lo cual, si bien realizamos la conexión entre ambas partes en el módulo de React,lo importante es darle relevancia a la manera de conectarnos con nuestra API y Debbugear todo lo necesario para que se comprenda como se realiza la conexión entre un back y un front , en especial para aquellos que no vieron como hacerlo. Todo lo relacionado a estilos y estructuras del Front quedarán en segundo plano y no deben ser codeadas, ya que para eso esta el módulo de Front-End.

## Archivos importantes

### utils.js y constants.js

En los archivos `utils.js` y `constants.js` encontraremos 3 variables de entorno que serán importantes para el desarrollo del proyecto.
Estas deben utilizarse en el archivo `.env`.

Las dejamos especificadas a continuación:

`export const  BASE_URL = 'http://localhost:8080' `; ( acá debemos reemplazar por la url de nuestra API deployada)

Por otro lado, tenemos otras dos, que son las mismas claves que declaramos en la API para los roles

`export const ADMIN = '50yun4dm1n';`

`export const USER = '50yunu53r';`

### Axios-issue.js y axios-user.js

En los archivos `axios-issue.js` y en `axios-user.js`, encontramos las peticiones a nuestra API (del tipo POST/PATCH), enviando todo lo que requerimos en los bodys y headers del POSTMAN.

### Navbar y Hero

En el componente `Navbar.jsx`, vamos a encontrar que nos traemos del STORE de Redux, a nuestro currentUser. Con eso mismo validamos que renderizar:

```
 {currentUser?.rol === ADMIN ? (
            <Link to='/issue'>Crear Issue</Link>
          ) : (
            <span>No podes crear un Issue</span>
)}
```

Además, en el `Hero.jsx` usamos al currentUser para validar más contenido.

```
{currentUser?.verified ? (
          <h1 className='title'>Bienvenido Usuario Verificado</h1>
        ) : (
          <div>
            <h1 className='title'>Tenes que validar tu cuenta</h1>
            <HeroFormStyled>
              <Button
                onClick={() => {
                  navigate('/validate');
                }}
                radius='10'
              >
                Validar usuario
              </Button>
            </HeroFormStyled>
          </div>
)}

```

### Pages

Luego, en TODAS las PAGES, exceptuando en la llamada `PageNotFound` , manejaremos peticiones a nuestra API:

Issue, ejecutamos createIssue. \
Login, ejecutamos loginUser.\
Register, ejecutamos createUser.\
Validate, ejecutamos verifyUser.\

### Login, Register y Validate

Tanto en LOGIN, REGISTER, Y VALIDATE ejecutamos 3 dispatch, estos mismos sirven para actualizar el estado del usuario en nuestro STORE de la aplicación en el Frontend.

Dentro de la carpeta redux/user podemos encontrar los dos slices que utiliza redux para actualizar el estado del usuario.

setCurrentUser para setear toda la información del usuario
setVerified para actualizar el campo verified del currentUser en true.

Nota: el slice toggleMenuHidden es necesario para que se abra el modal del home, NO ES NECESARIO DE EXPLICAR.
