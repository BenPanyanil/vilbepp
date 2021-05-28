<template>
    <div class="poster-description">
        <strong>Kuvaus</strong>
        <br>
        {{ content.description  }}
    </div>
</template>

<script>
export default {
    name: "DescriptionTab",
    props: {
        content: Object,
    }
}
</script>

<style scoped>
    .poster-description {
        height: calc(600px - 80px - 80px);
        padding: 0 25px;
    }
</style>