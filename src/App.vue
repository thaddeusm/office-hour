<template>
    <div id="app">
        <Meeting 
            v-if="meeting"
            v-on:close-meeting="reloadMeeting"
        />
        <div class="message" v-else>
            <h3 class="yellow-text">The meeting has ended.</h3>
        </div>
    </div>
</template>

<script>
import Meeting from '@/components/Meeting.vue'

export default {
    name: 'app',
    components: {
        Meeting,
    },
    data() {
        return {
            meeting: true
        }
    },
    methods: {
        reloadMeeting() {
            this.meeting = false

            let scope = this

            setTimeout(function() {
                scope.meeting = true
            }, 5000, scope)
        }
    }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
}

/* inspired by FHSU colors */
:root {
    --yellow: #FCBB04;
    --red: #D2360A;
    --black: #000000;
    --dark-gray: #040404;
    --gray: #6C6C6C;
    --light-gray: #E5E5E5;
    --white: #FFFFFF;
}

/* custom text highlight color */
::selection {
    background: var(--yellow);
}

html, body {
    width: 100%;
    height: 100%;
    background: var(--black);
}

body {
    height: 100vh;
    width: 100vw;
}

h1 {
    font-family: "ArchivoNarrow";
    -webkit-user-select: none;
    font-weight: 400;
    font-size: 2em;
}

h2 {
    font-family: "ArchivoNarrow";
    font-weight: 400;
    -webkit-user-select: none;
    font-size: 1.7em;
}

h3 {
    font-family: "ArchivoNarrow";
    font-weight: 500;
    -webkit-user-select: none;
    font-size: 1.5em;
}

h4 {
    font-family: "ArchivoNarrow";
    font-weight: 400;
    -webkit-user-select: none;
    font-size: 1.3em;
}

h5 {
    font-family: "ArchivoNarrow";
    font-weight: 400;
    -webkit-user-select: none;
    font-size: 1.2em;
}

h6 {
    font-family: "ArchivoNarrow";
    font-weight: 400;
    -webkit-user-select: none;
    font-size: 1.1em;
}

p {
    -webkit-user-select: none;
    font-family: "ArchivoNarrow";
    font-size: 1em;
    line-height: 1.5;
}

span {
    -webkit-user-select: none;
    font-family: "ArchivoNarrow";
}

li {
    -webkit-user-select: none;
    font-family: "ArchivoNarrow";
}

input[type=text], input[type=button] {
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    -webkit-border-radius: none;
    outline: none;
    border: none;
    font-family: "ArchivoNarrow";
}

input[type=text] {
    border-radius: 4px;
    font-size: 1.3em;
    padding: 7px 10px;
    color: var(--black);
    border: 1px solid var(--light-gray);
    outline: none;
}

*:focus {
    outline: 0 !important;
}

button {
    -webkit-user-select: none;
    -webkit-appearance: none;
    -moz-appearance: none;
    -webkit-border-radius: none;
    border: none;
    background: none;
    font-family: "ArchivoNarrow";
    outline: none;
    cursor: pointer;
}

button:disabled {
    opacity: .6;
    cursor: not-allowed;
}

a {
    -webkit-user-select: none;
    font-family: "ArchivoNarrow";
}

img {
    -webkit-user-select: none;
}

input {
    font-family: "ArchivoNarrow";
}

textarea {
    font-family: "ArchivoNarrow";
}

body {
    font-family: "ArchivoNarrow";
}

#app {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    -webkit-overflow-scrolling: touch;
    height: 100%;
    width: 100%;
}

.yellow-text {
    color: var(--yellow);
}

.message {
    display: grid;
    height: 100%;
    align-items: center;
    text-align: center;
}
</style>
