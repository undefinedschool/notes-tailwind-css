# ✨ Tailwind CSS

### 👉 Ver [todas las notas](https://github.com/undefinedschool/notes)

[Tailwind](https://tailwindcss.com/) es un _framework_ ([open-source](https://github.com/tailwindcss/tailwindcss)) no opinionado de CSS, que nos provee de _clases utilitarias_ para componer y usar a modo de bloques en nuestros maquetados, aplicando la filosofía de [CSS Funcional](https://github.com/dwyl/learn-tachyons#functional-css-is) o [Atomic CSS](https://www.youtube.com/watch?v=PcrzsCdoFoY). 

Funciona como un _plugin_ de [PostCSS](https://www.youtube.com/watch?v=bJShpMC7xFM), por lo que podemos integrarlo fácilmente con otras herramientas muy útiles, como [autoprefixer](https://github.com/postcss/autoprefixer) ó [PurgeCSS](https://www.purgecss.com/).

A diferencia de otros frameworks como [Bootstrap](https://getbootstrap.com/) ó [Bulma CSS](https://bulma.io/), **Tailwind no posee componentes con estilos predefinidos** (como _hero_, _button_, _card_, _navbar_, etc), por lo cual no nos veremos en el problema de estar sobre-escribiendo estilos luego si buscamos realizar diseños más customizados. Lo que nos provee en cambio, son clases utilitarias que podemos utilizar y componer para crear nuevas clases y estas a su vez, para crear nuestros propios componentes y estilos.

Este [_paradigma_](https://css-tricks.com/lets-define-exactly-atomic-css/) no plantea construir componentes con nuestro CSS, sino clases muy pequeñas con un objetivo bien definido, es decir, llevar el [principio de responsabilidad única](https://en.wikipedia.org/wiki/Single_responsibility_principle) al CSS. 

Para crear nuestros componentes, vamos a componer estas clases utilitarias (no estamos limitados a las que provee el framework, podemos extenderlas, modificarlas y agregar nuestras propias clases fácilmente) directamente en el HTML.

## Beneficios

- **No tenemos que pelear contra la especificidad del framework para redefinir estilos**
- **Tenemos mucho control sobre la especificidad**: al utilizar siempre estilos basados en clases y el approach _funcional_, nuestra UI termina siendo mucho más predecible y consistente
- **Descriptivo**: con leer el nombre de las clases entendemos qué está pasando
- Prácticamente no escribimos CSS
- **Evitamos la duplicación de código** utilizando _clases utilitarias_
- **Evitamos el _código zombie_**  usando plugins como [`purgecss`](https://github.com/undefinedschool/notes-tailwind-css#%EF%B8%8F-eliminar-css-redundante-con-purgecss)
- **Mobile-first, responsive design**: Tailwind cuenta con breakpoints predefinidos y es muy fácil aplicarlos a cualquier clase para tener [diseños totalmente _responsivos_](https://tailwindcss.com/docs/responsive-design/)
- **Productividad**: por todos los ítems anteriores, [desarrollar interfaces con Tailwind termina resultando mucho más eficiente](https://medium.com/@johnpolacek/by-the-numbers-a-year-and-half-with-atomic-css-39d75b1263b4), **escribimos mucho menos código y resulta mucho más fácil de mantener**

![](https://i.imgur.com/KZQyZtF.png)

## Características

- [Utility-first](https://tailwindcss.com/docs/utility-first)
- [Responsive Design](https://tailwindcss.com/docs/responsive-design)
- [Pseudo-Clases](https://tailwindcss.com/docs/pseudo-class-variants)
- [Base Styles](https://tailwindcss.com/docs/adding-base-styles)
- [Extraer Componentes](https://tailwindcss.com/docs/extracting-components)
- [Agregar nuevas clases utilitarias](https://tailwindcss.com/docs/adding-new-utilities)
- [Funciones y Directivas](https://tailwindcss.com/docs/functions-and-directives)

## Guías y tutoriales

- Ver la [documentación oficial](https://tailwindcss.com/docs/installation)
- ⭐️ [Screencasts](https://tailwindcss.com/screencasts/)
- [Introduction to Tailwind CSS](https://www.youtube.com/watch?v=O3JhdXubAK8)
- ⭐️ [Designing with Tailwind CSS](https://www.youtube.com/playlist?list=PL7CcGwsqRpSM3w9BT_21tUU8JN2SnyckR)
- [Why you don't need BEM with utility-first CSS](https://www.youtube.com/watch?v=ab8RePo5ZYU)
- [Adam Wathan - Tailwind CSS Best Practice Patterns](https://www.youtube.com/watch?v=J_7_mnFSLDg)

## Setup

```bash
npm init -y
```

Instalar el framework con _NPM_ (el ejemplo incluye PostCSS y algunos plugins, pero podemos instalar sólo `tailwindcss` si queremos):

```bash
npm i tailwindcss postcss-cli autoprefixer @fullhuman/postcss-purgecss cssnano
```

Es recomendable definir una estructura de directorios donde separemos `src` (donde estará el css base) y `dist` (donde estará el CSS compilado)

```
src
 |--- index.html
 |--- styles.css
dist
 |--- index.html
 |--- styles.css
```

Luego, agregar las [_directivas_](https://tailwindcss.com/docs/functions-and-directives/) a nuestro archivo css base (`styles.css` en el diagrama de arriba), que luego compilaremos

```css
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

### Crear `tailwind.config.js`

Este es el archivo que vamos a utilizar para sobreescribir (si es necesario) estilos default de Tailwind

```bash
npx tailwind init
```

### Crear `postcss.config.js`

- Ver [postcss-cli](https://github.com/postcss/postcss-cli)

#### Ejemplo de config (`postcss.config.js`)

```js
const tailwindcss = require('tailwindcss');
const autoprefixer = require('autoprefixer');
const cssnano = require('cssnano')({
  preset: 'default'
});
const purgecss = require('@fullhuman/postcss-purgecss')({
  content: ['./dist/*.html'],
  defaultExtractor: content => content.match(/[\w-/:]+(?<!:)/g) || []
});

module.exports = {
  plugins: [tailwindcss, autoprefixer, purgecss, cssnano]
};
```

Ahora podemos modificar el script de build para que use `postcss-cli`

```bash
"scripts": {
  "build:css": "postcss src/styles.css -o dist/compiled.css"
}
```

#### modo dev con `live-server`

1. Instalar de forma _global_ el módulo [`live-server`](https://www.npmjs.com/package/live-server)
2. Agregar el script `dev` a nuestro `package.json` para correr la aplicación en _modo desarrollo_

```bash
"scripts": {
  "build:css": "postcss src/styles.css -o dist/compiled.css",
  "dev": "live-server dist"
}
```

## VSCode Plugin

- ⭐️ **Recomendado:** instalar el plugin [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss) en VSCode

## ⭐️ Componentes

¿Qué pasa si nos encontramos [repitiendo ciertas combinaciones de clases continuamente](https://tailwindcss.com/docs/utility-first#maintainability-concerns)? Para evitar esto, podemos extraer los patrones de clases a **componentes**

- [Extracting Components](https://tailwindcss.com/docs/extracting-components/)
- [Extracting Reusable Components](https://tailwindcss.com/course/extracting-reusable-components/)
- [Components Examples](https://tailwindcss.com/components/)

### ⭐️ [tailwindcomponents](https://tailwindcomponents.com/): repositorio de componentes comunitario

### ⭐️ [Tailwind Toolbox](https://www.tailwindtoolbox.com/): templates, componentes y recursos

## Custom config

- Ejecutar `npx tailwind init` para generar el `tailwind.config.js`
- Ver [Configuration](https://tailwindcss.com/docs/configuration/)

## Extender Tailwind con nuevas clases

- Ver [How to Extend Tailwind CSS](https://www.youtube.com/watch?v=HVRnRp26_MQ)

## ⭐️ Eliminar CSS redundante con `PurgeCSS`

- `npm install -g postcss-cli`
- [How to setup Tailwind with PurgeCSS and PostCSS
](https://flaviocopes.com/tailwind-setup/)
- Ver [Designing with Tailwind CSS: Optimizing for Production with Purgecss
](https://www.youtube.com/watch?v=bhoDwo24K5Q)
- [Disabling unused utilities and variants](https://tailwindcss.com/docs/controlling-file-size#disabling-unused-utilities-and-variants)

## Recursos (imágenes, ilustraciones, íconos, etc)

- Ver [resources](https://tailwindcss.com/resources/)
- [Build with Tailwind](https://builtwithtailwind.com/)
