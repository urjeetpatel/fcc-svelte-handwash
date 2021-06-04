<script>
    import { createEventDispatcher } from "svelte";
    import { tweened } from "svelte/motion";
    import ProgressBar from "./ProgressBar.svelte";
    import { cubicOut } from "svelte/easing";

    let progress = tweened(0, { duration: 999, easing: cubicOut });
    const totalSeconds = 60;
    let elapsedSeconds = 0;
    let isActive = false;
    let dispatch = createEventDispatcher();

    $: secondsLeft = totalSeconds - elapsedSeconds;

    function timeTick() {
        elapsedSeconds += 1;
        progress.set((elapsedSeconds / totalSeconds) * 100);
        if (elapsedSeconds < totalSeconds && isActive) {
            setTimeout(timeTick, 1000);
        } else {
            isActive = false;
            elapsedSeconds = 0;
            progress.set((elapsedSeconds / totalSeconds) * 100);
            dispatch("end");
        }
    }

    function initTimer() {
        if (!isActive) {
            isActive = true;
            elapsedSeconds = 0;
            progress.set((elapsedSeconds / totalSeconds) * 100);
            setTimeout(timeTick, 1000);
        }
    }
</script>

<div bp="grid">
    <h2 bp="offset-4@md 6@md 12@sm">Seconds Left: {secondsLeft}</h2>
</div>
<ProgressBar progress={$progress} />
<div bp="grid">
    <button
        class="start"
        bp="offset-4@md 6@md 12@sm"
        on:click={initTimer}
        disabled={isActive}>Start</button
    >
</div>

<style>
    h2 {
        margin: 0;
    }
    .start {
        background-color: rgb(154, 73, 73);
        width: 100%;
        margin: 10px 0;
    }
    .start[disabled] {
        background-color: rgb(194, 194, 194);
        cursor: not-allowed;
    }
</style>
