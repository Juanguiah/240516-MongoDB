
# CRUD con MongoDB

## Insertar registros
```
db.personas.insert({
  nombres: 'Daniel',
  apellidos: 'Garces',
  edad: '45',
  intereses: ['bikes', 'cars'],
  direccion: {
    nombre: 'Casa',
    calle: '11'
  }
})
```

## Insertar multiples registros

```
db.personas.insertMany([
  {
  nombres: 'Daniel',
  apellidos: 'Garces',
  edad: '45',
  intereses: ['bikes', 'cars'],
  direccion: {
    nombre: 'Casa',
    calle: '11'
  }
},
{
  nombres: 'Jose',
  apellidos: 'Ospina',
  edad: '54',
  intereses: ['futbol'],
  direccion: {
    nombre: 'Oficina',
    calle: '29 con 87'
  }
}
])
```

## Actualizar un registro
En el siguiente ejemplo, vamos actualizar un registro existente, la función updateOne, recibe 2 argumentos, el primer argumento es el de búsqueda y el segundo argumento es el de actualización.
```
db.personas.updateOne(
  { "_id": ObjectId("615db43b8260347b1f95c321") },
  { "$set": { "intereses": ["novela", "ensayo"] } }
);

db.personas.updateOne(
  { "_id": ObjectId("615db43b8260347b1f95c321") },
  { "$set": { "apellidos": 'Gomez' } }
);

db.personas.update({ nombre: 'Daniel' },
{
  $set: {
    nombre: 'Juan',
    apellidos: 'Castillo'
  }
})
```

## Actualizar múltiples registros
En el siguiente ejemplo, vamos actualizar múltiples registros, la función updateMany, recibe 2 argumentos, el primer argumento es el de búsqueda y el segundo argumento es el de actualización, en este caso, buscará todos los documentos con esa coincidencia y aplicará la actualización sobre todos los documentos encontrados.
```
db.personas.updateMany(
  { "_id": ObjectId("615db43b8260347b1f95c321") },
  { "$set": { "intereses": ["novela", "ensayo"] } }
);

db.personas.updateMany(
  { "_id": ObjectId("615db43b8260347b1f95c321") },
  { "$set": { "apellidos": 'Gomez' } }
);
```

## Obtener todos los registros

```
db.personas.find({})
```

## Obtener todos los registros formateado

```
db.personas.find({}).pretty()
```

## Buscar registros - modo simple
Se pueden buscar registros, por cualquier atributo, debe tener coincidencia exacta
```
db.personas.find({ nombre: 'Daniel' })
db.personas.find({ _id: ObjectId('some-object-id') })
db.personas.find({ apellidos: 'Garces' })
```
Supongamos que se requiere buscar todos los registros que contengan una palabra en particular, esto es parecido a usar LIKE en sql.
```
db.personas.find({ nombre : /da/ })
db.personas.find({ nombre : /da/i }) -> con la i al final, estamos consiguiendo que sea insencible a mayúsculas y minúsculas
```


## Ordenando registros 

```
# Orden ascendente
db.personas.find().sort({ nombre: 1 }).pretty()
# Orden descendente
db.personas.find().sort({ nombre: -1 }).pretty()
```

## Contar registros

```
db.personas.find({}).count()
db.personas.find({ nombre: 'Daniel' }).count()
```

## Limitar registros

```
db.personas.find({}).limit(2).pretty()
```

## Encadenando una busqueda
En el siguiente ejemplo vamos a limitar la busqueda de registros a 2 y al mismo tiempo ordenando de forma ascendente.
```
db.personas.find().limit(2).sort({ nombre: 1 }).pretty()
```

## Buscar el primer registro

```
db.personas.findOne({ nombre: 'Daniel' })
```

## Búsqueda de un registro, seleccionando ciertos campos en la respuesta.
El siguiente ejemplo, es similiar como haríamos un select en sql, ej: Select nombre, apellidos, edad from personas where nombre = 'Daniel';
```
db.personas.find({ nombre: 'Daniel' }, {
  nombre: 1,
  apellidos: 1,
  edad: 1
})
```

## Renombrando un campo específico

```
db.personas.update({ nombre: 'Daniel' },
{
  $rename: {
    apellidos: 'apellido'
  }
})
```

## Eliminar un registro

```
db.personas.remove({ nombre: 'Daniel' })
```

## Eliminar todos los registros

```
db.personas.deleteMany({})
```
