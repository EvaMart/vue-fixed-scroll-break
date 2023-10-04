<template>
    <div id="main-div" ref="toTop">
        <slot />
    </div>
</template>
<script>

export default {
    name: 'VueFixedScrollBreak',
    beforeMount() {
        window.addEventListener('scroll', this.handleScroll);
    },
    unmounted() {
		window.removeEventListener('scroll', this.handleScroll);
	},
    methods: {
        goToTopPosition() {
            /* 
            ---- We can use a ref that can be passed somehow to the component ---- 
			const refFooter = this.$root.$children[2].$refs.Footer;
			const topOfFooter = refFooter.$el.offsetTop;
            */

            // ---- Or we can use a static value ----
            const topOfFooter = 2355 // PROPERTY: top of footer

			const bottom = window.scrollY + window.innerHeight;
			const distanceFromFooter = bottom - topOfFooter;

            
			if (bottom < topOfFooter + 120) { // PROPERTY: distance from footer to stop. TotalOffset. 120 is the distance from the footer to stop the button
				this.$refs.toTop.$el.style.bottom = `${120}px`; // PROPERTY: distance from footer to stop.  TotalOffset.
			} else {
				this.$refs.toTop.$el.style.bottom = `${distanceFromFooter}px`;
			}
		},

        handleScroll() {
			this.goToTopPosition(); // GoToTop button position -> stop at footer
		},
    }
}

</script>

<style>

#main-div {
    position: fixed;
    top: 200;
    color: red;
}

</style>