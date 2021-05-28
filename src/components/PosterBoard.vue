<template>
    <section>
        <div v-if="!data.length" class="no-notices">Ei uusia ilmoituksia!</div>
        <div v-else class="notice-board-container">
            <poster
                v-for="post in data"
                :key="post.id"
                :post="post">
            </poster>
        </div>
    </section>
</template>

<script>
import Poster from './poster-components/Poster.vue'

export default {
    name: "PosterBoard",
    components: { 
        Poster 
    },
    props: {
        data: Array,
    }
}
</script>

<style scoped>
    .notice-board-container {
        min-width: 900px;
        min-height: 100vh;
		width: 50vw;
		margin: 0 auto;
		padding: 100px 0;	
        /* background-color: white; */

        display: grid;
        grid-template-columns: repeat(1, 1fr);
        grid-template-rows: auto;
        gap: 40px;
	}
    .no-notices {
        min-width: 900px;
        min-height: 100vh;
		width: 50vw;
		margin: 0 auto;
		padding: 150px 0;	
        font-size: 4rem;
        font-weight: bold;
        text-align: center;
    }
    @media only screen and (min-width: 800px) {
        .notice-board-container {
            grid-template-columns: repeat(2, 1fr);
        }
        .notice-board-container > .poster-canvas:nth-child(even) {
            transform: translateY(50px);
        }
    }
    @media only screen and (min-width: 1900px) {
        .notice-board-container {
            grid-template-columns: repeat(3, 1fr);
        }
        .notice-board-container > .poster-canvas:nth-child(odd) {
            transform: translateY(50px);
        }
    }
</style>