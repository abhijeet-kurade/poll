<script>
    import Card from "../shared/Card.svelte";
    import {createEventDispatcher} from 'svelte';
    export let poll = {};
    $: totalVotes = poll.voteA + poll.voteB;
    const dispatch = createEventDispatcher();

    const castVote = (option, id) =>{
        dispatch('voting', {option, id});
    }
    // $:{
    //     let percentA = Math.floor(100/totalVotes*poll.voteA);
    //     let percentB = Math.floor(100/totalVotes*poll.voteB);
    // }
    $: percentA = Math.floor(100/totalVotes*poll.voteA);
    $: percentB= Math.floor(100/totalVotes*poll.voteB);
</script>


<Card>
    <div class="poll">
        <h3>{poll.question}</h3>
        <p>Total Votes: {totalVotes}</p>
        <div class="answer" on:click={()=> castVote('a', poll.id) }>
            <div class="percent percent-a" style="width: {percentA}%;"></div>
            <span>{poll.answerA} ({poll.voteA})</span>
        </div>
        <div class="answer" on:click={()=> castVote('b', poll.id) }>
            <div class="percent percent-b" style="width: {percentB}%;"></div>
            <span>{poll.answerB} ({poll.voteB})</span>
        </div>
    </div>
</Card>


<style>
    h3{
        margin: 0 auto;
        color: #555;
    }
    p{
        margin-top: 6px;
        font-size: 14px;
        color: #aaa;
        margin-bottom: 30px;
    }
    .answer{
        background: #fafafa;
        cursor: pointer;
        margin: 10px auto;
        position: relative;
    }
    .answer:hover{
        opacity: 0.6;
    }
    span{
        display: inline-block;
        padding: 10px 20px;
    }
    .percent{
        height: 100%;
        position: absolute;
        box-sizing: border-box;
    }
    .percent-a{
        border-left: 4px solid #d91b42;
        background: rgba(217, 27, 66, 0.2);
    }
    .percent-b{
        border-left: 4px solid #454545;
        background: rgba(69, 196, 150, 0.2);
    }


</style>