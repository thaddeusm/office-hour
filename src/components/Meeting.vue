<template>
	<div class="container">
		<header>
			<vue-webrtc 
	            width="100%" 
	            ref="webrtc"
	            :roomId="roomId" 
	            :socketURL="server"
	            v-on:joined-room="status = 'streaming'"
	            v-on:left-room="logEvent"
	            v-on:open-room="logEvent"
	        >
	        </vue-webrtc>
		</header>
		<main>
			<button v-if="status == 'streaming'" class="yellow block-button" @click="leaveMeeting">Leave</button>
			<Loader size="large" v-else-if="status == 'joined'" />
			<button v-else-if="status == 'disconnected'" class="yellow block-button" @click="joinMeeting">Join</button>
		</main>
        <footer>
        	
        </footer>
	</div>
</template>

<script>
import * as io from 'socket.io-client'
window.io = io

import Loader from '@/components/Loader.vue'

export default {
	name: 'Meeting',
	components: {
		Loader
	},
	data() {
        return {
            roomId: '0000',
            server: 'https://office-hour-server.seatsmart.tech/',
            status: 'disconnected'
        }
    },
    methods: {
        joinMeeting() {
        	this.status = 'joined'
            this.$refs.webrtc.join()
        },
        leaveMeeting() {
            this.status = 'disconnected'
            this.$refs.webrtc.leave()
        },
        logError(error, stream) {
            console.log('On Error Event', error, stream)
        },
        logEvent(event) {
            console.log('Event : ', event)
        }
    }
}
</script>

<style>
.container {
	text-align: center;
	height: 100%;
	min-height: 100vh;
	width: 100%;
	display: grid;
	grid-template-rows: 160px 1fr 160px;
	grid-template-areas: 
		"header"
		"main"
		"footer";
	align-items: center;
}

header {
	grid-area: header;
}

main {
	grid-area: main;
}

footer {
	grid-area: footer;
}

.video-list {
    background: var(--black)!important;
}

.video-item {
	background: var(--black)!important;
}

.video-item:first-child {
	position: fixed;
	bottom: 0;
	right: 0;
}

.video-item:first-child > video {
	border: 3px solid var(--red)!important;
}

button {
	padding: 5px 10px;
	font-size: 18px;
	border-radius: 5px;
	cursor: pointer;
	border: 1px solid var(--gray);
	margin-top: 20px;
  	margin-left: 10px;
  	margin-right: 10px;
  	outline: none;
}

.block-button {
	display: block;
	margin: 0 auto;
}

.yellow {
	background: var(--yellow);
	color: var(--black);
}

.gray {
	background: var(--light-gray);
	color: var(--black);

}
</style>