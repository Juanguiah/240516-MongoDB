# MongoDB - Comandos básicos en la shell

## Mostrar todas las bases de datos

```
show dbs
```

## Mostrar la base de datos actual
```
db
```
## Cambiarse de base de datos

```
use testdatabase
```

## Borrar base de datos - borra la base de datos actual, sobre la que esté usando
```
db.dropDatabase()
```
## Crear una colección de datos
```
db.createCollection('personas')
```
## Borrar una colección de datos
```
db.nombreColeccion.drop()
```

## Mostrar las colecciones de datos
```
show collections
```
