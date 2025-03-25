# CS LM Questionnaire

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) to make the TypeScript language service aware of `.vue` types.

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

# How to

## Come metto un campo required?

Aggiungo alla classe del componente il campo `required`. Esempio:

```html
<cs-input v-model="name" label="Nome" required></cs-input>
```

Per avere una ui che indichi che il campo è obbligatorio, aggiungo la classe `validator` al componente. Esempio:
Vedi la documentazione di daisyui per ulteriori l'uso nei specifici componenti: https://daisyui.com/components/validator/

```html
<select class="select validator">
  <option value="" disabled selected>Seleziona un'opzione</option>
  <option value="1">Opzione 1</option>
  <option value="2">Opzione 2</option>
</select>
```
