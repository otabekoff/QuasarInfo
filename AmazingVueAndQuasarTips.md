**v-text** - *v-text attribute element in VueJS helps to render any text coming from data, API or backend.
but not look like v-html it doesn't render as HTML or predefined code*.

**v-directives(v-text & more)** - *https://vuejs.org/v2/api/#v-text*

**Class: Ellipsis** - *this class is equal of the CSS ellipsis like below:*

```css
div.b {
  white-space: nowrap; 
  width: 50px; 
  overflow: hidden;
  text-overflow: ellipsis; 
  border: 1px solid #000000;
}
```

*and used to add ... if the text is more than container size. Usage: can use with 1,2,3 lines of code:*

**ellipsis**

**ellipsis-2-lines**

**ellipsis-3-lines**

*For more go here: https://quasar.dev/style/visibility#Introduction*

*And usage in action: https://codepen.io/Impeccable-Ninja/pen/eYpdxam*


**V-Bind** - *V-bind is a tool for sending all data from parent to the child. And to receive data we need to create props.
And in genereal we use like this v-bind="products". In this way we send full data. Imgine we have 5 products in an array called products:[] and it has keys of id, pic, name, info, price, bonus. Then we need to send it to a component. For instance that component name is hello. And we write:* ``<hello v-bind="products"``*. This is in the parent. And in the child we need to create props. In genereal we write props after* ``export default {}``. Ok now we have prop like this:

```js
export default {
  props: {
    products: {
      type: Array,
      default: {}
    }
  }
}
```

*Here we are getting **Array** of products, so we specify the type of the prop as an **Array**. Don't forget to write it with capital letters. Here we need to set defaults if no data. Empty array look is {} in general so we write empty array in order not to get error or disappering of the component. OK, We get the data but how to use? How? As it was in general before. Yes with v-for or binding. For instance:*

```html
<div v-for="product in products" :key="product.id">
  <p>{{product.id}} - product</p>
  <img :src="product.pic">
  <p>{{product.name + ' ' + product.price}}</p>
  <p>{{product.info}} has {{bonus}} bonuses.</p>
</div>
```
*That's it. It is what we need to know about **v-bind** for now.*
