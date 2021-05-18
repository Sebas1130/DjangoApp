# DjangoApp

### Resumen de las Clase de Django

Comparto aquí un resumen de la clase espero les sea útil:

>Las opciones que Django propone para implementar Usuarios personalizados son:

	Usando el Modelo proxy
	Extendiendo la clase abstracta de Usuario existente
	Para el presente proyecto debemos crear los campos de usuario:

>Luego debemos crear la app que se llamará users :

	python manage.py startapp users 

 >Se debe importar lo que necesitamos

	from django.contrib.auth.models import User 

>Luego se crea los campos adicionales que se necesitan según el proyecto

## Profile Model.
Modelo proxy que amplía los datos base con otra información

>class Profle (models.Model):   

	user=models.OneToOneField(User,on_delete=models.CASCADE)
	website=models.URLField(max_length=200,blank=True)
	biography=models.TextField(blank=True)
	phone_number=models.CharField(max_length=20,blank=True) 
	picture=models.ImageField( upload_to='users/pictures', blank=True, null=True )
	create=models.DateTimeField(auto_now_add=True)
	modified=models.DateTimeField(auto_now=True)

>def __str__(self):
    """Return username."""
    return self.user.username

Posterior a eso dirigirse al archivo de settings.py y así como se instaló post se va a instalar users

#####  Para que funcione el campo ImageField se debe instalar la librería Pillow y se lo hace de la siguiente manera

	sudo pip install Pillow 
	Despues ejecutar para que se hagan efecto las migraciones
	python3 manage.py makemigrations python3 manage.py migrate 

##### para ingresar al administrador de django crear el super usuario

	python3 manage.py createsuperuser

# Patrones de Diseño de DJANGO

ORM: Object-relational mapping. Es el encargado de permitir el acceso y control de una base de datos relacional a través de una abstracción a clases y objetos.

Templates: Archivos HTML que permiten la inclusión y ejecución de lógica especial para la presentación de datos.

* Modelo: Parte de un proyecto de Django que se encarga de estructurar las tablas y propiedades de la base de datos a través de clases de Python.

* Vista: Parte de un proyecto de Django que se encarga de la lógica de negocio y es la conexión entre el template y el modelo.

* App: Conjunto de código que se encarga de resolver una parte muy específica del proyecto, contiene sus modelos, vistas, urls, etc.

## Patrón de diseño: Solución común a un problema particular.

Los Middlewares tienen el siguiente orden:

	SecurityMiddleware: Se encarga de comprobar todas las medidas de seguridad, las variables de settings relacionadas con Https, Auth, entre otros.
	SessionMiddleware:  Se encarga de validar una sesión.
	CommonMiddleware: Se encarga de verificar componentes comunes como lo es el debug.
	CsrfViewMiddleware: Se encarga de toda la validación correspondiente a CSRF. Éste nos permite utilizar el tag {% csrf_token %} y es el que inserta el token de seguridad en cada formulario.
	AuthenticationMiddleware: Nos permite agregar request.user desde las vistas.
	MessageMiddleware: Pertenece al Framework de mensajes de Django, y permite pasar un mensaje sin necesidad de mantener un estado en la base de datos o en memoria.
	XFrameOptionsMiddleware: Middleware de seguridad
