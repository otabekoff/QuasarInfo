# Installing the VueI18N language switch
[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

###### To install manually write ``npm install yarn --save`` or ``yarn add i18n --save``.But, Note that! When Quasar project was created (during the installation) it was isntalled. If you're creating new project just click or select the ``vue18n`` with space keyboard key.
#
#### To set the VueI18N correctly
> Note that the following files will be automatically created with the project if you selected them during the installation. Just if you don't see them. Then create these files.

  **1. Create a `i18n.js` boot file in `src/boot/` folder.**
  ```js
  import Vue from 'vue'
    import VueI18n from 'vue-i18n'
    import messages from 'src/i18n'
    
    Vue.use(VueI18n)
    
    const i18n = new VueI18n({
      locale: 'en-us',
      fallbackLocale: 'en-us',
      messages
    })
    
    export default ({ app }) => {
      // Set i18n instance on app
      app.i18n = i18n
    }
    
    export { i18n }
```
  **2. Import above `i18n.js` boot file in `quasar.conf.js` file.**
###### Even this is specified in newer versions of Quasar. If you don't see such kind of  `i18n.js` import go to the  `quasar.conf.js` file then look for the `boot` section. Then write this in it.
#
```js
    boot: [
      'i18n',
    ],
```
###### Then go to the `build` section. and find something related to `webpack`. Then replace that part with the following code:
#
```js
      extendWebpack (cfg) {
        cfg.module.rules.push({
          resourceQuery: /blockType=i18n/,
          use: [
            {loader: '@kazupon/vue-i18n-loader'},
            {loader: 'yaml-loader'}
          ]
        })
      }
```

###### But in general and newly created project it will look like the following code so replace it with the above code:
#
```js
      extendWebpack (cfg) {
      }
```

###### ***Just setting VueI18N language switch has finished. Now we'll set languages.***
#
#### Setting VueI18N local languages file and folders
> Note: these all files are already created but just we must replace, edit, delete some of the and create new files and folders.
  1. Go ``src/i18n`` if there is no such path create it.
  2. Create lang code folders and ``index.js`` files in that folders like this structure:
```
----------------------------------
>-- src/                          |
    >-- i18n/                     |
        >-- en-us/                |
            > index.JS            |
        >-- uz-lat/               |
            > index.JS            |
        >-- ru-rus/               |
            > index.JS            |
    > index.js                    |
----------------------------------
```
  3. Then go ``src/i18n/index.js`` file and update it like this:
```js
import enUS from './en-us'
import uzLat from './uz-lat'
import ruRus from './ru-rus'

export default {
  'en-us': enUS,
  'uz-lat': uzLat,
  'ru-rus': ruRus
}
```
###### ***Now we imported the ``index.js`` language files from their folder inside the main ``index.js`` file.***
###### ***So, we we'll see how to write the index.js files in the language folders.***
#
### How to write the language translation (``index.js``) files!
> Note: All the keys of the `index.js` files inside of the language folders are the same, but their values are the same with the language folder and the language which you are writing them in your `index.js` folder. So, please provide everything like below.

  - Here is the looks of the index files in language folders:
##### index.js file for `en-us` folder.
#
```js
// This is just an example,
// so you can safely delete all default props below

export default {
  welcomeMessage: 'Welcome to Quasar',
  partingMessage: 'See you soon at Quasar'
}
```

##### index.js file for `ru-rus` folder.

```js
// This is just an example,
// so you can safely delete all default props below

export default {
    welcomeMessage: 'Добро пожаловать в Квазар',
    partingMessage: 'До скорой встречи в Квазаре'
  }
  ```

##### index.js file for `uz-lat` folder.
#
```js
// This is just an example,
// so you can safely delete all default props below

export default {
    welcomeMessage: 'Quasarga xush kelibsiz',
    partingMessage: 'Yaqinda Quasarda ko\'rishguncha'
  }
```

###### ***So as you see inside of ``index.js`` files above we only write a ``keyword`` and give it a ``value`` and export them only. And we just provide correct translations according to the language folder and file. Next, let's see how to change them. The most interesting part.***
#
#
#### Changing the languages with select (In Quasar framework).
> So just go to the the `index.vue` file (**this is for testing purposes only when you are working on languages you just can edit and put it in everywhere you want**) and look there will be this look of code inside that `index.vue` file:
```html
<template>
  <q-page class="column justify-center items-center">
    <q-select
    v-model="lang"
    :options="langOptions"
    label="Quasar Language"
    dense
    borderless
    emit-value
    map-options
    options-dense
    style="min-width: 150px"
  />
    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-full.svg"
    >
    <p class="text-h3 q-mt-md">{{ $t('welcomeMessage') }}</p>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data() {
    return {
      lang: this.$i18n.locale,
      langOptions: [
        { value: 'en-us', label: 'English' },
        { value: 'uz-lat', label: 'Uzbek' },
        { value: 'ru-rus', label: 'Russian' }
      ]
    }
  },
  watch: {
    lang(lang) {
      this.$i18n.locale = lang
    }
  }
}
</script>
```
> Note: Here, as you are seeing there is a template section(for HTML), a script section(for JavaScript and VueJS) and a Style section(for any CSS pre-processors or just CSS).

###### In the ``template`` part you're seeing the select options. And there is ``:options: langOptions``. By writing this we are getting the informations from ``script`` part by binding to the ``langOptions`` data. And in the ``script`` section you're seeing the language options. Here we specify the language keys(Which were imported and exported in ``src/i18n/index.js`` file) as values. And just we are setting their display name inside of the label as `English`, `Uzbek` and `Russian` for Quasar Select Option. One line above of the `langOptions` data, we see the lang data which is helping us to get values from `I18N`.
###### So, let's continue? OK, Just we can see something called ``watch`` life cycle hook which runs everything in it before the website begin loading. In it we are watching for lang function which equalizes ``this.$i18n.locale`` to `lang`. Here we launched the `vue18n`. And in the `template` section we should display the different language word values. But how? To display values as vue has with ``{{ welcomeMessage }}``? No we just don't do like that. But we write something that looks like that: `` {{  $t('welcomeMessage') }}``. Because we are getting `welcomeMessage` key and their values that were already in the language files as a function. And Quasar select option is giving us the opportunity of changing languages by selecting them from options list. So if we select `English` we see ``Welcome to Quasar`` and if we select `Uzbek` we see ``Quasarga xush kelibsiz`` and if we again select the third option, `Russian` we see `Добро пожаловать в Квазар`. Just that's it.
#
#
#
> Note: if you want to give the language word keys(that were written in the language files) in `script` part, use them in this style. ``this.$t('welcomeMessage')``

### Just we fully finished installing and working with I18N.