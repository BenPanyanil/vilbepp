<template>
    <div class="poster-functions">
        <div class="poster-functions-header">
            <div class="title">{{ content.title }}</div>
            <div class="close" @click="closeContent">X</div>    
        </div>
        <description-tab
            v-if="posterState === 'description'"
            :content="content">
        </description-tab>
        <participants-tab             
            v-else-if="posterState === 'participants'"
            :content="content">
        </participants-tab>
        <chat-tab
            v-else-if="posterState === 'chat'"
            :content="content">
        </chat-tab>
    </div>
</template>

<script>
import ChatTab from './ChatTab.vue'
import DescriptionTab from './DescriptionTab.vue'
import ParticipantsTab from './ParticipantsTab.vue'

export default {
    name: "PosterFunctions",
    components: { DescriptionTab, ChatTab, ParticipantsTab },
    props: {
        content: Object,
        posterState: String,
    },
    methods: {
        closeContent: function () {
            this.$emit('update:posterState', '')
        },
    }
}
</script>

<style scoped>
    .poster-functions {
        position: relative;
        height: calc(600px - 80px);
        background: white;
    }
    .poster-functions-header {
        height: 80px;
        padding: 0 25px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .title {
        font-size: 1.2rem;
        font-weight: bold;
    }
    .close {
        height: 30px;
        width: 30px;
        border-radius: 100%;

        display: flex;
        justify-content: center;
        align-items: center;

        cursor: pointer;
    }
    .close:hover {
        background: #444444;
        color: white;
    }
</style>