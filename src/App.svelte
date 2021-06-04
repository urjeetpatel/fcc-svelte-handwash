<script>
    import HowTo from "./components/HowTo.svelte";
    import Timer from "./components/Timer.svelte";

    let audio;

    function EndTimer() {
        audio.play();
    }
</script>

<h1>Handwashing App</h1>
<Timer on:end={EndTimer} />
<HowTo />
<!-- svelte-ignore a11y-media-has-caption -->
<audio bind:this={audio}>
    <source src="sound.mp3" type="audio/mp3" />
    Your browser does not support the audio element.
</audio>

<style>
    h1 {
        text-align: center;
    }
</style>
