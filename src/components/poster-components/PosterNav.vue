<template>
    <div class="poster-nav">
        <div class="poster-nav-item">
            <div class="avatar"></div>
            <div class="name">{{ user.name }}</div>
        </div>
        <div class="poster-nav-item">
            <div class="poster-nav-btn" :class="{active: posterState === 'description'}" @click="setPosterState('description')">Ku</div>
            <div class="poster-nav-btn" :class="{active: posterState === 'participants'}" @click="setPosterState('participants')">Os</div>
            <div class="poster-nav-btn" :class="{active: posterState === 'chat'}" @click="setPosterState('chat')">Ke</div>
            <div class="poster-nav-btn">P</div>
        </div>
    </div>
</template>

<script>
export default {
    name: "PosterNav",
    props: {
        user: Object,
        posterState: String
    },
    methods: {
        setPosterState: function (state) {
            this.$emit('update:posterState', state)
        }
    }
}
</script>

<style>
    .poster-nav {
        height: 80px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 20px;
    }
    .poster-nav-item {
        display: flex;
        align-items: center;
        gap: 15px;
    }
    .avatar {
        width: 40px;
        height: 40px;
        border-radius: 100%;
        background: #d3d3d3;
    }
    .name {
        position: relative;
    }
    .name:before {
        content: 'Ilmoittaja';
        position: absolute;
        top: -14px;
        font-size: 0.75rem;
        opacity: 0.5;
    }
    .poster-nav-btn {
        cursor: pointer;
    }
    .poster-nav-btn.active {
        border-bottom: 2px solid;
    }
</style>