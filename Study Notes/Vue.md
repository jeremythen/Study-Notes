

Vuex is like Redux, but for Vue.




# Binding:

v-bind:src="image_attr_in_vue_instance"
or

:src="image"
:href="url"

:disabled="boolean"

etc.

## Class binding

:class="{disabledButton: !inStock}"


# Showing or not conditionally

## v-if, else if and v-else

<p v-if="isLoading">Loading</p>
<p v-else-if="value > 10 && value > 5">Loading</p>
<p v-else="isLoading">Loading</p>

These remove the element from the DOM.

## v-show="boolean"

This only hides it, which is more efficient than the others. It adds display: none.


# Looping

v-for="details in details" where details is in the vue instance.

Use the :key, as in React.

<span v-for="detail in details" :key="detail.id">...</span>


## Event

v-on:click

<button v-on:click="cart += 1">Add to Cart</button>
<button v-on:click="addToCart">Add to Cart</button>

```javascript
var app = new Vue({
    el: '#app',
    data: {
        product: 'Socks',
        add: 0
    },
    methods: { // Where you put your methods.
        addToCart: function() {
            this.cart += 1
        },
        updateProduct() {
        //
        }
    },
    computed: {
        title() {
            return this.brand ' ' + this.product
        }
    }
    
})
```

<product @mouseover="updateProduct(variant.variantImage)">...

### Other events

* @mouseover
* @submit
* @keyup.enter // With a modifier


## Style binding

:style={backgroundColor: variant.color }

:style="{[style1, style2]}" // With multiple style objects.

These values will be in the 'data' field of the Vue instance.

# Computed properties

{{ title }} // This will call title() in the computed field. This is cached until any of the original values changes.


# Components

Pass props

```javascript
Vue.component('componentName', {
    //props: [message], For simple props
    props: {
        message: {
            type: String,
            required: true,
            default: "Hi"
        }
    },
    template: `
        <div>
            {{ message }}
        </div>
    `,
    data() {
        return {
            product: 'Socks',
            brand: 'Vue Mastery',
            ...
        }
    }
}

```


In HTMl, use it like:

<product :message="The Message"></product>


# Communicating Events


In the product component

```javascript
addToCart() {
    this.$emit('add-to-cart')
}
```

<product @add-to-cart="updateCart"></product> // This will call it's parent updateCart method.


# Forms and two-way data binding

Use v-model="propertyname"

v-model.number="rating" // This .number will make sure to cast it to an int.

@submit
or
@submit.prevent

let eventBus = new Vue({

})

```javascript
Vue.component('product-review', {
    template: `
    <form @submit.prevent="onSubmit">
        <input v-model="name">
    </form>
    `,
    data() {
        return {
            name: null
        }
    },
    methods: {
        onSubmit() {
            /// this.name...
        }
    },
    mounted() { // A life cycle method.
        ///
        eventBus.$on('review-submitted', productReview => { // Using that Vue instance as an event emitter.
            //
        })
    }
}
```

In a .vue file, write vue and hit enter to get a template auto generated.

