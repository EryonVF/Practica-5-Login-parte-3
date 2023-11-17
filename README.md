
Sesiones en Flask
En el contexto del desarrollo web, una sesión en Flask es una forma de almacenar información del usuario de manera persistente entre diferentes solicitudes HTTP durante la visita de un usuario a un sitio web. Las sesiones permiten recordar información específica del usuario mientras navegan entre páginas o realizan acciones en el sitio.

Identificación del Usuario
La identificación del usuario se logra mediante el uso de un identificador único llamado "ID de sesión", que generalmente se almacena en una cookie en el navegador del usuario. Este ID de sesión único se utiliza para asociar la información específica del usuario almacenada en el servidor con la sesión del usuario.

Estado del Usuario
Las sesiones permiten que un sitio web "recuerde" el estado del usuario. Por ejemplo, si un usuario inicia sesión, la información de inicio de sesión puede almacenarse en la sesión para que el usuario no tenga que volver a iniciar sesión en cada página.

Autenticación de Usuarios y Sesiones en Flask
En Flask, la autenticación de usuarios y la gestión de sesiones se simplifican con la extensión Flask-Login. Esta extensión proporciona clases y funciones que facilitan la autenticación y el manejo de sesiones de usuario.

Instalar Flask-Login:

Copy code
pip install Flask-Login
Configurar LoginManager en Flask:

python
Copy code
from flask_login import LoginManager

app = Flask(__name__)
login_manager = LoginManager(app)
Login y Logout de Usuarios:

La función login_user se utiliza para iniciar sesión a un usuario después de verificar sus credenciales.
La función logout_user se utiliza para cerrar la sesión de un usuario.
Reconociendo al Usuario:

Después de iniciar sesión, puedes reconocer al usuario en las plantillas de Flask utilizando la variable current_user. Por ejemplo:
html
Copy code
<h1>Bienvenido, {{ current_user.fullname }}</h1>
Bloqueo de Páginas para Usuarios no Administradores:

Puedes usar el decorador @admin_required para bloquear el acceso a páginas que solo deben ser accesibles por administradores.
python
Copy code
from functools import wraps
from flask import abort

def admin_required(func):
    @wraps(func)
    def decorated_view(*args, **kwargs):
        if not current_user.is_authenticated or current_user.usertype != 1:
            abort(403)  # Acceso prohibido
        return func(*args, **kwargs)
    return decorated_view
Bloqueo de Páginas para Usuarios no Autentificados:

Puedes usar el decorador @login_required para bloquear el acceso a páginas que solo deben ser accesibles por usuarios autentificados.
python
Copy code
from flask_login import login_required

@app.route("/ruta")
@login_required
def ruta_protegida():
    return "Esta ruta está protegida"
Estos son conceptos clave para implementar sesiones, autenticación de usuarios y controles de acceso en Flask. Asegúrate de personalizar estos conceptos según las necesidades específicas de tu aplicación.
