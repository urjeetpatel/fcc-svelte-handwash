<script>
    export let progress = 0;
</script>

<div bp="grid">
    <div class="progress-container" bp="offset-4@md 6@md 12@sm">
        <div class="progress-bar" style="width:{progress}%;">
            <span class="sr-only">{progress}%</span>
        </div>
    </div>
</div>

<style>
    .progress-container {
        margin: 20px 0;
        border: solid rgb(194, 194, 194) 1px;
    }
    .progress-bar {
        height: 30px;
        background-color: rgb(77, 199, 55);
    }
</style>
