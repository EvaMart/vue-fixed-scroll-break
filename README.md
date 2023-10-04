# vue-fixed-scroll-break

A wrapper component to make an element fixed and stop it from scrolling past a certain point.

## Passing reference of component to stop at.

```html
<VueFixedScrollBreak
    :offset-ref="'#my-reference'"
    :additional-offset="100"
    >
    My content
</VueFixedScrollBreak>
```

Example:
A vuetify button to go to top of page. `ref` of footer is `Footer`
```html
<template>
    <VueFixedScrollBreak
        :offset-ref="footerRef"
        :additional-offset="100"
        >
            <v-btn
                id="to-top"
                ref="toTop"
                class="mx-2"
                fab
                dark
                small
                color="#f48f43"
				>
					<v-icon dark> mdi-arrow-up </v-icon>
				</v-btn>
    </VueFixedScrollBreak>

    <div ref="Footer">
        My footer
    </div>
    
</template>

<script>
import 'VueFixedScrollBreak' from 'vue-fixed-scroll-break'

export default {
    name: 'MyGoToTopButton'
    components: {
        VueFixedScrollBreak
    },
    data() {
        return {
            footerRef : this.$refs.Footer
        }
    },

}

</script>
```
In this case the button will stop scrolling when it reaches 100px from the footer.

> :bulb: this example assumes the footer is in the same component as the button. If not, you will need to use an expression similar to this one to get the reference of the footer: 
>    ```html
>    footerRef: this.$root.$children[2].$refs.Footer
>    ```


## Passing position directly (TotalOffset) (in pixels)
```html
<VueFixedScrollBreak
    :offset="'100'"
    >
    My content
</VueFixedScrollBreak>
```
