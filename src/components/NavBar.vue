<template>
    <nav>
        <div class="justify-between">
            <p class="button">VilBepp</p>
            <p class="button" @click="openCreatePost">Luo ilmoitus</p>
        </div>
    </nav>
</template>

<script>
export default {
    name: "Nav",
    methods: {
        openCreatePost: function () {
            this.$emit("update:openCreatePost", true)
        }
    }
}
</script>

<style>
    nav {
        position: fixed;
        z-index: 9999;
        background-color: white;
        width: 100vw;
        padding: 5px 40px;
    }
    .justify-between {
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .button {
        cursor: pointer;
    }
</style>