<script>
    import Poll from "./PollDetails.svelte";

    export let polls = [];

</script>

<div class="poll-list">
    {#each polls as poll (poll.id) }
        <div><Poll {poll}  on:voting/></div>
    {/each}
</div>

<style>
    .poll-list{
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;

    }

</style>