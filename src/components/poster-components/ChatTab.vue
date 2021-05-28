<template>
    <div class="poster-chat-system">
        <div ref="scroll-container" class="scroll-container">
            <div class="chat-pool">
                <div v-for="bubble in messageBubbles" :key="bubble.id" class="bubble" :class="{me: bubble.isMe}">{{ bubble.text }}</div>
            </div>
        </div>
        <div class="input-bar">
            <input placeholder="kirjoita..." v-model="message" @keyup.enter="sendMessage" type="text">
            <span class="send-btn" @click="sendMessage">></span>
        </div>
    </div>
</template>

<script>
export default {
    name: "ChatTab",
    props: {
        content: Object,
    },
    data: function () {
        return {
            messageBubbles: [],
            message: '',
        }
    },
    methods: {
        sendMessage: function () {
            if (!this.message || !this.message.trim().length) {
                this.message = ''
                return
            }

            const formattedMessage = this.message.charAt(0).toUpperCase() + this.message.slice(1);
            const messagePkg = {isMe: true, text: formattedMessage}
            this.messageBubbles.push(messagePkg)
            this.message = ''
        },
        scrollToEnd: function () {
            const scrollContainer = this.$refs['scroll-container']
            scrollContainer.scrollTo(0, scrollContainer.scrollHeight)
        },
    },
    watch: {
        messageBubbles: function () {
            this.scrollToEnd()
        }
    }
}
</script>

<style scoped>
    .poster-chat-system {
        height: calc(600px - 80px - 80px);
        display: flex;
        flex-direction: column;
    }

    /* Styling for post title section  */
    .post-title {
        width: 100%;
        padding: 20px;
        background-color: white;
        border-bottom: 1px solid;
    }

    /* Styling for chat pool */
    .scroll-container {
        background-color: #C3FEFA;
        width: 100%;
        height: 100%;
        padding: 0 20px;

        overflow: auto;
    }
    .chat-pool {
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
        padding: 10px 0;
    }
    .bubble.me {
        display: inline-block;
        max-width: 70%;
        margin: 4px 0;
        padding: 6px 18px;
        margin-left: auto;
        border-radius: 5px;
        background-color: #444444;

        color: white;
        word-wrap: break-word;
        overflow-wrap: anywhere;
        hyphens: auto;
        white-space: normal;
    }
    .bubble {
        margin-right: auto;
    }

    /* Styling for input section */
    .input-bar {
        z-index: 99;
        width: 100%;
        padding: 15px;
        background: white;

        display: flex;
        align-items: center;
        flex: 1;
        gap: 8px;
    }
    input[type="text"] {
        padding: 5px 10px;
        width: 100%;
    }
    input[type="text"]:focus {
        outline: none;
    }
    .send-btn {
        min-width: 35px;
        min-height: 35px;
        border-radius: 100%;

        display: flex;
        justify-content: center;
        align-items: center;

        background-color: #444444;
        color: white;

        cursor: pointer;
    }
</style>