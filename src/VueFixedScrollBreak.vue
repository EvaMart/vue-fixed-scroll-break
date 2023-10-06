<template>
    <div :style="style()" >
        <slot />
    </div>
</template>
<script>

export default {
    name: 'VueFixedScrollBreak',
    props: {
        totalOffset: {
            type: Number,
            default: 80,
            required: false
        },
        topOfStopElement: {
            type: Number,
            required: true
        },

    },
    data() {
        return {
            offset:  this.totalOffset,
        }
    },
    beforeMount() {
        window.addEventListener('scroll', this.handleScroll);
    },
    unmounted() {
		window.removeEventListener('scroll', this.handleScroll);
	},
    methods: {
        goToTopPosition() {

			const bottom = window.scrollY + window.innerHeight;
			const distanceFromStopElement = bottom - this.topOfStopElement;

            //---------------------------------------------
            // Make diagram of this:
            console.log('bottom', bottom)
            console.log('this.topOfStopElement', this.topOfStopElement)
            console.log('distanceFromStopElement', distanceFromStopElement)
            console.log('this.totalOffset', this.totalOffset)
            //---------------------------------------------

            // topOfStopElement +  totalOffset = distance from footer to stop
			if (bottom < this.topOfStopElement + this.totalOffset) { 
                // the component has not reached the limit 
				this.offset = this.totalOffset  
			} else {
                // the component reached the limit 
				this.offset = distanceFromStopElement;
			}
		},

        style(){
            return {
                bottom: `${this.offset}px !important`,
                position: 'fixed',
            }
        },

        handleScroll() {
            console.log('Scrolling!')
			this.goToTopPosition();
		},
    }
}

</script>
