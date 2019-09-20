<template>
    <div id="app">
        <vue-webrtc 
            width="100%" 
            ref="webrtc"
            :roomId="roomId" 
            v-if="roomId !== ''"
            :socketURL="server"
            v-on:joined-room="logEvent"
            v-on:left-room="logEvent"
            v-on:open-room="logEvent"
            v-on:share-started="logEvent"
            v-on:share-stopped="logEvent"
        >
        </vue-webrtc>
        <button @click="onJoin">Join</button>
    </div>
</template>

<script>
import * as io from 'socket.io-client'
window.io = io

export default {
    name: 'app',
    data() {
        return {
            roomId: '0000',
            server: 'https://office-hour-server.seatsmart.tech/'
        }
    },
    methods: {
        onCapture() {
            this.img = this.$refs.webrtc.capture();
        },
        onJoin() {
            this.$refs.webrtc.join();
        },
        onLeave() {
            this.$refs.webrtc.leave();
        },
        onShareScreen() {
            this.img = this.$refs.webrtc.shareScreen();
        },
        onError(error, stream) {
            console.log('On Error Event', error, stream);
        },
        logEvent(event) {
            console.log('Event : ', event);
        },
    }
}
</script>

<style>

</style>
