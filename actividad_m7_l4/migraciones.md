# Comprensión teórica

## ¿Qué es una migración en Django?

Una migración es un archivo que guarda los cambios que hacemos en los modelos para que esos cambios también se apliquen a la base de datos.

## ¿Qué problema soluciona respecto a los cambios en los modelos?

Permite mantener la base de datos actualizada cada vez que agregamos, eliminamos o modificamos campos en los modelos, sin tener que hacer los cambios manualmente.

## ¿Por qué no basta con modificar el archivo `models.py` directamente sin hacer migraciones?

Porque cambiar el archivo `models.py` solo modifica el código del proyecto. La base de datos no se actualiza automáticamente, por lo que hay que crear y aplicar las migraciones para que ambos queden sincronizados.

## Describe lo que sucede si no aplicas una migración pendiente

Si no aplicamos una migración pendiente, los cambios realizados en los modelos no se reflejan en la base de datos. Esto puede provocar errores al ejecutar la aplicación, ya que Django intentará acceder a tablas o columnas que todavía no existen o que no están actualizadas.

## python manage.py showmigrations

El comando `python manage.py showmigrations` muestra todas las migraciones que existen para cada aplicación del proyecto, indicando cuáles ya fueron aplicadas y cuáles están pendientes.

Las migraciones que aparecen con **[X]** significa que ya fueron ejecutadas correctamente y sus cambios ya están reflejados en la base de datos. En cambio, si una migración apareciera con **[ ]**, significaría que aún no ha sido aplicada y sería necesario ejecutar `python manage.py migrate`.

![Showmigrations](/img/m7_l4.png)