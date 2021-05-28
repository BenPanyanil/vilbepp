<template>
    <div class="poster-canvas">
        <div class="poster-background">
            <poster-content
                v-if="!posterState"
                :content="post.postContent">
            </poster-content>
            <poster-functions
                v-else
                :content="post.postContent"
                :posterState.sync="posterState">
            </poster-functions>
        </div>
        <poster-nav 
            :user="post.user"
            :posterState.sync="posterState">
        </poster-nav>
    </div>
</template>

<script>
import PosterContent from './PosterContent.vue'
import PosterFunctions from './PosterFunctions.vue'
import PosterNav from './PosterNav.vue'

export default {
    name: "Poster",
    components: { PosterNav, PosterFunctions, PosterContent },
    props: {
        post: Object
    },
    data: function () {
        return {
            posterState: '',
        }
    },
    computed: {
        fetchBackgroundImage: function () {
            // const background = this.post.postContent.imageURL ? "backgroundImage: `url(${ post.postContent.imageURL })`" : "background-color: 'white'"
            const background = "'background-color': '#ffffff'"
            return background
        }
    },
}
</script>

<style>
    .poster-canvas {
        height: 600px;
		/* background: #ffffff; */
        border: 1px solid;
        /* box-shadow: 0 2px 6px rgba(0,0,0,0.1); */
	}
    .poster-background {
        position: relative;
        height: calc(600px - 80px);

        background-image: url("../../assets/kahvi.jpeg");
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
    }
</style>