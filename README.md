# [WIP] notes-tailwind-css

[Tailwind](https://tailwindcss.com/) es un _framework_ no opinionado de CSS, que nos provee de _clases utilitarias_ para componer y usar a modo de bloques en nuestros maquetados, aplicando la filosofía de [CSS Funcional](https://github.com/dwyl/learn-tachyons#functional-css-is).

A diferencia de otros frameworks como [Bootstrap](https://getbootstrap.com/) ó [Bulma CSS](https://bulma.io/), Tailwind no posee componentes con estilos predefinidos, por lo cual no nos veremos en el problema de estar sobre-escribiendo estilos luego si buscamos diseños más customizados. Lo que nos provee en cambio, son clases utilitarias que podemos utilizar y componer para crear nuevas clases y estas a su vez, para crear nuestros propios componentes y estilos.

## Setup

Primero debemos instalar el framework con _NPM_:

```bash
npm i tailwindcss
```

Es recomendable definir una estructura de directorios donde separemos `src` (donde estará el css base) y `dist` (donde estará el CSS compilado)

```
src
 |--- styles.css
dist
 |--- index.html
 |--- compiled.css
```

Luego, agregar las _directivas_ a nuestro archivo css base (`styles.css` en el diagrama de arriba), que luego compilaremos

```
@tailwind base;

@tailwind components;

@tailwind utilities;
```

Agregar al `package.json`, en la sección de `scripts`, un script para compilar y generar el CSS

```json
"scripts": {
  "build:css": "tailwind build src/styles.css -o dist/compiled.css"
}
```

## Componentes

## Eliminar CSS redundante

Ver [Removing unused CSS](https://tailwindcss.com/docs/controlling-file-size#removing-unused-css)
