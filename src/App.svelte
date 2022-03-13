<script>
	import Header from "../src/components/Header.svelte";
	import Footer from "../src/components/Footer.svelte";
	import Polls from "../src/components/Polls.svelte";
	import CreatePollForm from "../src/components/CreatePollForm.svelte";
	import Tabs from "./shared/Tabs.svelte";

	//tabs
	let items = ['Current Polls', 'Add New Poll'];
	let activeItem = 'Current Polls';
	const tabChnage = (e) => {		
		activeItem = e.detail;	
	}

	let polls = [
        {
            id : 1,
            question : 'Frontend or Backend ?',
            answerA : 'Frontend',
            answerB : 'Backend',
            voteA : 9,
            voteB : 15,
        },
    ];
	
	const addPoll = (e) => {
		polls = [e.detail, ...polls];
		console.log(polls);
		activeItem = 'Current Polls';
	}
	const castVote = (e) => {
		let {id, option} = e.detail;
		let copy = [...polls];
		let upVotedPoll = copy.find((upPoll)=> upPoll.id == id );
		if(option === 'a'){
			upVotedPoll.voteA += 1;
		}
		if(option === 'b'){
			upVotedPoll.voteB += 1;
		}
		polls = copy;
	}

</script>

<Header />
<main>
	<Tabs {items} {activeItem} on:tabChnage={tabChnage}/>
	{#if activeItem == 'Current Polls'}
	<Polls {polls} on:voting={castVote}/>
	{:else if activeItem == 'Add New Poll'}
	<CreatePollForm on:addPoll={addPoll}/>
	{/if}
</main>
<Footer />

<style>
	main{
		width: 100%;
		max-width: 960px;
		margin: 40px auto;
	}
	
</style>