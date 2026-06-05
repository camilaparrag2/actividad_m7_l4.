# Actividad_m7_l2: Conexión a Base de Datos y Uso del ORM en Django

## 1. Conexión a PostgreSQL

### Instalación del controlador PostgreSQL

Para permitir que Django se conecte a PostgreSQL, se instaló el siguiente paquete:

```bash
pip install psycopg2-binary
```

### Creación de la base de datos

Se creó una base de datos vacía llamada `libreria` en PostgreSQL:

```sql
CREATE DATABASE libreria;
```

### Configuración en settings.py

Se modificó el archivo `settings.py` para utilizar PostgreSQL como motor de base de datos.

> **Importante:** Las credenciales mostradas son de ejemplo y no corresponden a credenciales reales.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'libreria',
        'USER': 'usuario',
        'PASSWORD': '1234',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

---

## 2. Definición del Modelo

Se creó el modelo `Libro` dentro de la aplicación principal.

```python
from django.db import models

class Libro(models.Model):
    titulo = models.CharField(max_length=100)
    autor = models.CharField(max_length=50)
    anio_publicacion = models.IntegerField()
    disponible = models.BooleanField(default=True)
```

### Clave primaria por defecto

Django crea automáticamente un campo llamado `id` de tipo `AutoField`, el cual funciona como clave primaria cuando no se define una explícitamente.

```python
id = models.AutoField(primary_key=True)
```

### Clave primaria compuesta

Django no soporta claves primarias compuestas de forma nativa. Sin embargo, se puede simular utilizando una restricción de unicidad sobre varios campos.

Ejemplo:

```python
class Libro(models.Model):
    titulo = models.CharField(max_length=100)
    autor = models.CharField(max_length=50)

    class Meta:
        unique_together = ('titulo', 'autor')
```

Esto impide que existan dos registros con la misma combinación de título y autor.

---

## 3. Aplicación de Migraciones

### Crear migraciones

```bash
python manage.py makemigrations
```

**¿Qué hace?**

Analiza los modelos definidos en la aplicación y genera archivos de migración con los cambios detectados.

### Aplicar migraciones

```bash
python manage.py migrate
```

**¿Qué hace?**

Ejecuta las migraciones pendientes y crea o actualiza las tablas correspondientes en la base de datos.

---

## 4. Operaciones CRUD utilizando el ORM de Django

Para realizar las operaciones se utilizó la shell de Django.

### Ingresar a la shell

```bash
python manage.py shell
```

### Importar el modelo

```python
from libreria.models import Libro
```

---

### Crear un nuevo libro (Create)

```python
Libro.objects.create(
    titulo="cien años de soledad",
    autor="gabriela garcia marquez",
    anio_publicacion=1967
)

Libro.objects.create(
    titulo="el secreto",
    autor="rhonda byrne",
    anio_publicacion=2006
)

Libro.objects.create(
    titulo="tan poca vida",
    autor="hanya yanagihara",
    anio_publicacion=2016
)

Libro.objects.create(
    titulo="la tregua",
    autor="mario benedetti",
    anio_publicacion=2015
)
```

Resultado:

```python
<Libro: Libro object (1)>
<Libro: Libro object (2)>
<Libro: Libro object (3)>
<Libro: Libro object (4)>
```

---

### Listar todos los libros (Read)

```python
Libro.objects.all()
```

Resultado:

```python
<QuerySet [
    <Libro: Libro object (1)>,
    <Libro: Libro object (2)>,
    <Libro: Libro object (3)>,
    <Libro: Libro object (4)>
]>
```

---

### Buscar un libro por su título (Read)

```python
Libro.objects.get(titulo="tan poca vida")
```

Resultado:

```python
<Libro: Libro object (3)>
```

---

### Actualizar el campo disponible de un libro (Update)

Se obtuvo el libro con ID 2 y se modificó el campo `disponible` a `False`.

```python
libro = Libro.objects.get(id=2)
libro.disponible = False
libro.save()
```

**Explicación:**

- `get(id=2)` obtiene el libro específico.
- Se modifica el valor del campo `disponible`.
- `save()` guarda los cambios en la base de datos.

---

### Eliminar un libro (Delete)

Se eliminó el libro con ID 4.

```python
libro = Libro.objects.get(id=4)
libro.delete()
```

Resultado:

```python
(1, {'libreria.Libro': 1})
```

**Explicación:**

- `get(id=4)` obtiene el libro que se desea eliminar.
- `delete()` elimina el registro de la base de datos.
- El resultado indica que se eliminó un registro del modelo `Libro`.

---


