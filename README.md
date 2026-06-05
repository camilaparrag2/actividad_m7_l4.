# basedatos_django


from libreria.models import Libro

Crear un nuevo libro

>>> Libro.objects.create(titulo="cien años de soledad", autor="gabriela garcia marquez", anio_publicacion=1967)
<Libro: Libro object (1)>
>>> Libro.objects.create(titulo="el secreto", autor="rhonda byrne", anio_publicacion=2006)
<Libro: Libro object (2)>
>>> Libro.objects.create(titulo="tan poca vida", autor="hanya yanagihara", anio_publicacion=2016)
<Libro: Libro object (3)>
>>> Libro.objects.create(titulo="la tregua", autor="mario benedetti", anio_publicacion=2015)
<Libro: Libro object (4)>

Listar todos los libros

>>> Libro.objects.all()
<QuerySet [<Libro: Libro object (1)>, <Libro: Libro object (2)>, <Libro: Libro object (3)>, <Libro: Libro object (4)>]>

Buscar un libro por su título

>>> Libro.objects.get(titulo="tan poca vida")
<Libro: Libro object (3)>

Actualizar el campo disponible de un libro

>>> libro = Libro.objects.get(id=2)
>>> libro.disponible = False
>>> libro.save()

Eliminar un libro

>>> libro = Libro.objects.get(id=4)
>>> libro.delete()
(1, {'libreria.Libro': 1})
>>> 