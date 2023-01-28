<script lang="ts">
    import {onMount} from "svelte";

    let pc;

    function init(): void{
        const iceServers={
            iceServers:[
                {
                    urls:["stun:stun1.l.google.com:19302", "stun:stun2.l.google.com:19302"]
                }
            ], icecandidatePoolSize:10
        }

        pc = new RTCPeerConnection(iceServers);
    }

    async function connect(){
        pc.onicecandidate = (e) => {
            if(e.candidate){
                console.log(e.candidate);
            }
        }

        const offer = await pc.createOffer();
        await pc.setLocalDescription(offer);
        console.log("offer", offer);
    }


    onMount(()=>{
        init();
    })

</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
<button on:click={connect}>
    Click Me!
</button>