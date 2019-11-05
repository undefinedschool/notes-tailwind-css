# notes-tailwind-css

[Tailwind](https://tailwindcss.com/) es un _framework_ no opinionado de CSS, que nos provee de _clases utilitarias_ para componer y usar a modo de bloques en nuestros maquetados, aplicando la filosofía de [CSS Funcional](https://github.com/dwyl/learn-tachyons#functional-css-is) o [Atomic CSS](https://www.youtube.com/watch?v=PcrzsCdoFoY).

A diferencia de otros frameworks como [Bootstrap](https://getbootstrap.com/) ó [Bulma CSS](https://bulma.io/), Tailwind no posee componentes con estilos predefinidos, por lo cual no nos veremos en el problema de estar sobre-escribiendo estilos luego si buscamos realizar diseños más customizados. Lo que nos provee en cambio, son clases utilitarias que podemos utilizar y componer para crear nuevas clases y estas a su vez, para crear nuestros propios componentes y estilos.

Este [_paradigma_](https://css-tricks.com/lets-define-exactly-atomic-css/) no plantea construir componentes con nuestro CSS, sino clases muy pequeñas con un objetivo bien definido, es decir, llevar el [principio de responsabilidad única](https://en.wikipedia.org/wiki/Single_responsibility_principle) al CSS. 

Para crear nuestros componentes, vamos a componer estas clases utilitarias (no estamos limitados a las que provee el framework, podemos extenderlas, modificarlas y agregar nuestras propias clases fácilmente) directamente en el HTML.

## Guías y tutoriales

- Ver la [documentación oficial](https://tailwindcss.com/docs/installation)
- [Screencasts](https://tailwindcss.com/screencasts/)
- [Adam Wathan - Tailwind CSS Best Practice Patterns](https://www.youtube.com/watch?v=J_7_mnFSLDg)

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

### Ejemplo de script

```json
"scripts": {
  "build:css": "tailwind build src/styles.css -o dist/compiled.css"
}
```

## Componentes



Ver [Components Examples](https://tailwindcss.com/components/)

## Eliminar CSS redundante

Ver [Removing unused CSS](https://tailwindcss.com/docs/controlling-file-size#removing-unused-css)
