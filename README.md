
# vue-fixed-scroll-break

A wrapper component to make an element fixed and stop it from scrolling past a certain point.


## Installation

```bash
npm install vue-fixed-scroll-break
```

## Usage

```html
<VueFixedScrollBreak>
    My content
</VueFixedScrollBreak>
```


## Props

| Name | Type | Required| Default | Description |
| --- | --- | --- | --- | --- |
| `topOfStopElement` | Number | Yes | - | The offset from the top of the stop element to stop scrolling. |
| `totalOffset` | Number | 80 | No | An additional distance from the `topStopElement` to stop scrolling. |



## Example
This example is a vuetify button to go to top of page. The button will stop scrolling when it reaches the footer.  

The property `topOfStopElement` is calculated from the offset of the footer element. Using a `ref` in the footer is a simple and straightforward way to calculate it using `this.$refs.Footer.$el.offsetTop`. 



```html
<template>
    <VueFixedScrollBreak
		:top-of-stop-element="offset"
        :total-offset="100"
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
            offset: this.$refs.Footer.$el.offsetTop;
        }
    },

}

</script>
```
In this case the button will stop scrolling when it reaches 100px from the top of the footer.

> :bulb: In this example the footer is in the same component as the button. If this were not the case, it would still be possible to access it through `this.$root.$children`. 

