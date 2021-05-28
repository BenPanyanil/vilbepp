<template>
    <div>
        <div class="poster-main-title">{{ content.title }}</div>
    </div>
</template>

<script>
export default {
    name: "PosterContent",
    props: {
        content: Object
    }
}
</script>

<style>
    .poster-main-title {
        position: absolute;
        top: 80px;
        left: 50%;
        transform: translateX(-50%);
        padding: 10px 20px;
        background: white;
        box-shadow: 0 0 6px rgba(0,0,0,0.2);
    }
</style>