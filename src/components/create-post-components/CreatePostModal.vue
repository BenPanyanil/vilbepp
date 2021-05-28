<template>
    <div class="create-post-overview">
        <div class="overlay" @click="close"></div>
        <div class="modal">
            <div class="modal-header">
                <div class="title">Luo uusi ilmoitus</div>
                <div class="close" @click="close">X</div>
            </div>
            <div class="modal-body">
                <div>
                    <div class="input-label">Otsikko</div>
                    <input v-model="title" type="text">
                </div>
                <div>
                    <div class="input-label">Kuvaus</div>
                    <textarea name="message" v-model="description" rows="10" cols="30"></textarea>
                </div>
            </div>
            <div class="modal-footer">
                <div class="create-btn" @click="submit" @keyup.enter="submit">Luo ilmoitus!</div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios"

export default {
    name: "CreatePostModal",
    props: {
        data: Array
    },
    data: function () {
        return {
            title: '',
            description: '',
        }
    },
    methods: {
        close: function () {
            this.$emit("update:openCreatePost", false)
        },
        submit: function () {
            if (!this.title || !this.description) return

            const postObject = {
                user: {
                    name: "Ben"
                },
                postContent: {
                    title: this.title,
                    description: this.description,
                    imageURL: ""
                }
            }

            axios
                .post('http://localhost:3001/posts', postObject)
                .then(response => {
                    const posterData = response.data
                    this.$emit('update:data', this.data.push(posterData))
            })

            this.title = ''
            this.description = ''
            this.close()
        }
    }
}
</script>

<style scoped>
    .overlay {
        position: fixed;
        z-index: 9999;
        inset: 0;
        background-color: rgba(0,0,0,0.7);
    }
    .modal {
        position: fixed;
        top: 15vh;
        left: 50vw;
        transform: translateX(-50%);
        z-index: 10000;
        width: 600px;
        height: 600px;
        padding: 0 40px;

        background-color: #efefef;
        overflow: auto;

        /* box-shadow: 0 2px 30px rgba(0,0,0,0.3); */
        border: 1px solid;
    }
    .modal-header {
        height: 80px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .modal-body {
        height: calc(600px - 80px - 100px);
        display: flex;
        flex-direction: column;
        gap: 10px;
    }
    .modal-footer {
        height: 100px;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .title {
        font-size: 1.2rem;
        font-weight: bold;
    }
    .input-label {
        margin: 5px 0;
    }
    .create-btn {
        padding: 10px 50px;
        border-radius: 100px;
        background-color: #444444;
        color: white;
        text-align: center;
        cursor: pointer;
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
    input[type="text"] {
        padding: 5px 10px;
        width: 100%;
    }
    input[type="text"]:focus {
        outline: none;
    }
    textarea {
        padding: 5px 10px;
        width: 100%;
    }
    textarea:focus {
        outline: none;
    }
</style>