# Nucba Zappi 🍕

En este repositorio se encuentra el proyecto final del módulo de Backend, integrado con un Front simplificado. Este mismo no tiene grande funcionalidades, ya que su principal objetivo es mostrar como interactuamos con nuestra API desde un entorno que no sea el POSTMAN.

Debemos recordar que no todos los alumnos cursaron el módulo de FrontEnd, y es más importante darle relevancia a la manera de conectarnos con nuestra API y debugear todo lo necesario para comprenderlo. Los estilos y estructuras del FrontEnd quedan en segundo plano, Y NO DEBEN SER CODEADAS.

Archivos a tener en cuenta: 

En utils/constants.js vamos a encontrar tres variables de entorno importantes a usar ( estas deben usarse en un archivo .env, pero se muestran acá para fines prácticos )

export const BASE_URL = 'http://localhost:8080'; ( acá debemos reemplazar por la url de nuestra API deployada)

Estas son las mismas claves que declaramos en la API para los roles 
export const ADMIN = '50yun4dm1n';
export const USER = '50yunu53r';

Luego en axios-issue.js y en axios-user.js, encontramos las peticiones a nuestra API (del tipo POST/PATCH), enviando todo lo que requerimos en los bodys y headers del POSTMAN.

En el componente Navbar.jsx, vamos a encontrar que nos traemos del STORE de Redux, a nuestro currentUser, con eso mismo validamos que renderizar. 

 {currentUser?.rol === ADMIN ? (
            <Link to='/issue'>Crear Issue</Link>
          ) : (
            <span>No podes crear un Issue</span>
)}

Al igual que en el hero, usamos al currentUser para validar más contenido.

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

En cuanto a las PAGES, menos en la PageNotFound, luego en todas manejaremos peticiones a nuestra API.

Issue, ejecutamos  createIssue.
Login, ejecutamos  loginUser.
Register, ejecutamos createUser.
Validate, ejecutamos verifyUser. 

Tanto en LOGIN, REGISTER, Y VALIDATE ejecutamos 3 dispatch, estos mismos sirven para actualizar el estado del usuario en nuestro STORE de la aplicación en el Frontend. 

Dentro de la carpeta redux/user podemos encontrar los dos slices que utiliza redux para actualizar el estado del usuario. 

setCurrentUser para setear toda la información del usuario
setVerified para actualizar el campo verified del currentUser en true. 
