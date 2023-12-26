# JavaScript

## Common methods

### Filter
```js
const usuarios = [
  { nombre: "Marta", edad: 29, activo: true },
  { nombre: "Juan", edad: 42, activo: false },
  { nombre: "Sofía", edad: 35, activo: true }
];

const usuariosActivosMayoresDe30 = usuarios.filter(usuario => usuario.activo && usuario.edad > 30);
// Resultado: [{ nombre: "Sofía", edad: 35, activo: true }]
```

### Map
```js
const empleados = [
  { nombre: "Ana", salario: 3000, departamento: "IT" },
  { nombre: "Luis", salario: 4000, departamento: "Marketing" },
  { nombre: "Carlos", salario: 5000, departamento: "IT" }
];

const aumentos = empleados.map(empleado => {
  let aumento = 0;
  if (empleado.departamento === "IT") {
    aumento = empleado.salario * 0.1;
  } else if (empleado.salario < 4500) {
    aumento = empleado.salario * 0.05;
  }
  return { ...empleado, salario: empleado.salario + aumento };
});
```

### Iterate objects
```js
const object1 = {
  a: 'somestring',
  b: 42,
};

for (const [key, value] of Object.entries(object1)) {
  console.log(`${key}: ${value}`);
}

// Expected output:
// "a: somestring"
// "b: 42


// For IN Uses the object’s key And use as index


const user = {
    name: 'John Doe',
    email: 'john.doe@example.com',
    age: 25,
    dob: '08/02/1989',
    active: true
};

// iterate over the user object
for (const key in user) {
    console.log(`${key}: ${user[key]}`);
}
```

### Object.assign
```ts
async update(id: string, updateUsuarioDto: UpdateUsuarioDto): Promise<{ usuario: UsuarioDto }> {
    const user = await this.usuarioRepository.findOne({ where: { id } });
    if (!user) {
        throw new HttpException(`Usuario not found`, HttpStatus.NOT_FOUND);
    }
    Object.assign(user, updateUsuarioDto);
    const updatedUser = await this.usuarioRepository.save(user);
    return { usuario: toUsuarioDto(updatedUser) };
}
```

El uso de `Object.assign` en tu función de actualización no causará que el objeto quede incompleto si no se pasan todos los atributos. Aquí te explico cómo funciona y por qué tu implementación es correcta en este contexto:

1. **Funcionamiento de `Object.assign`**: Este método copia todas las propiedades enumerables de uno o más objetos fuente a un objeto destino. Si una propiedad en el objeto fuente tiene un valor `undefined`, no sobrescribirá una propiedad existente en el objeto destino.
2. **Tu Código**: En tu función `update`, primero recuperas el usuario existente con `this.usuarioRepository.findOne({ where: { id } });`. Este paso obtiene un objeto usuario completo desde la base de datos.
3. **Actualización de Propiedades**: Luego, utilizas `Object.assign(user, updateUsuarioDto);` para actualizar este objeto usuario. Aquí, `updateUsuarioDto` contiene las propiedades que deseas cambiar. Las propiedades en `updateUsuarioDto` sobrescribirán las correspondientes en el objeto `user`, pero
   solo para las propiedades que están presentes en `updateUsuarioDto`. Si `updateUsuarioDto` no incluye alguna propiedad, el valor original en `user` permanecerá intacto.
4. **Resultado**: El resultado es que solo se actualizan las propiedades que se pasan en `updateUsuarioDto`. Las propiedades que no están en `updateUsuarioDto` no se verán afectadas y conservarán sus valores originales.

En resumen, tu uso de `Object.assign` es apropiado para actualizar un subconjunto de propiedades de un objeto. No causará que el objeto esté incompleto si no se pasan todos los atributos; solo actualizará las propiedades que se proporcionen en `updateUsuarioDto`.

Objeto Usuario Original (user) obtenido de la base de datos { id: "123", username: "originalUsername", email: "originalEmail@example.com", password: "hashedPassword123" }

Objeto con Actualizaciones (updateUsuarioDto) { email: "newEmail@example.com" }

Después de aplicar Object.assign Object.assign(user, updateUsuarioDto);

Objeto Usuario Actualizado (user) { id: "123", username: "originalUsername", email: "newEmail@example.com", // <- Actualizado password: "hashedPassword123" }


### Reduce
```js
const frutas = ["manzana", "plátano", "manzana", "naranja", "plátano", "manzana"];

const conteoFrutas = frutas.reduce((acumulador, fruta) => {
  acumulador[fruta] = (acumulador[fruta] || 0) + 1;
  return acumulador;
}, {});

// conteoFrutas será: { manzana: 3, plátano: 2, naranja: 1 }
```

### Sort
```js
const productos = [
  { nombre: "Manzana", precio: 1.2 },
  { nombre: "Plátano", precio: 0.8 },
  { nombre: "Manzana", precio: 1.0 }
];

productos.sort((a, b) => {
  if (a.nombre < b.nombre) return -1;
  if (a.nombre > b.nombre) return 1;
  return a.precio - b.precio;
});
// Ordena primero por nombre, y luego por precio dentro del mismo nombre
```