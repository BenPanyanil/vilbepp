<template>
	<div id="app">
		<nav-bar :openCreatePost.sync="openCreatePost"></nav-bar>
		<poster-board :data="dataInverted"></poster-board>
		<create-post-modal 
			v-if="openCreatePost" 
			:openCreatePost.sync="openCreatePost"
			:data.sync="data">
		</create-post-modal>
	</div>
</template>
<script>
import PosterBoard from './components/PosterBoard.vue'
import NavBar from './components/NavBar.vue'
import axios from "axios"
import CreatePostModal from './components/create-post-components/CreatePostModal.vue'

export default {
	name: 'App',
	components: {
		NavBar,
		PosterBoard,
		CreatePostModal
	},
	data: function () {
		return {
			data: [],
			openCreatePost: false,
		}
	},
	computed: {
		dataInverted: function () {
			const reversed = this.data.slice().reverse()
			return reversed
		}
	},
	mounted: async function () {
		await this.fetchData()
	},
	methods: {
		fetchData: async function () {
			await axios
				.get('http://localhost:3001/posts')
				.then(response => {
					this.data = response.data
			})
		}
	}
}
</script>

<style>
	* {
		font-family: 'Poppins', sans-serif;
		color: #444444;
		box-sizing: border-box;
	}
	body {
		margin: 0;
		background: #efefef;
	}
</style>