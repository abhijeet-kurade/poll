<script>

    import {createEventDispatcher} from 'svelte';
    import Button from "../shared/Button.svelte";

    let fields ={question:'', answerA:'', answerB:''};
    let errors ={question:'', answerA:'', answerB:''};
    
    let dispatch = createEventDispatcher();

    let valide = false;

 

    const submitHandler = () => {
        valide = true;

        // validate question
        if(fields.question.trim().length < 5){
            valide = false;
            errors.question = 'Question must be at least 5 char long';
        }
        else{
            errors.question = '';
        }


        // answer a
        if(fields.answerA.trim().length < 1){
            valide = false;
            errors.answerA = 'Answer must be at least 1 char long';
        }
        else{
            errors.answerA = '';
        }

        // answer b
        if(fields.answerB.trim().length < 1){
            valide = false;
            errors.answerB = 'Answer must be at least 1 char long';
        }
        else{
            errors.answerB = '';
        }

        if(valide){            
            let poll ={...fields, voteA :0, voteB :0, id:Math.random()};
            dispatch('addPoll', poll);
        }
        else{
            console.log(errors);
        }
    }

</script>

<form on:submit|preventDefault={submitHandler}>
    <div class="form-field">
        <label for="question">Quetion: </label>
        <input type="text" id="question" bind:value={fields.question} class:redBorder={errors.question.length != 0}>
        <div class="error">{errors.question}</div>
    </div>

    <div class="form-field">
        <label for="answer-a">Answer A: </label>
        <input type="text" id="answer-a" bind:value={fields.answerA} class:redBorder={errors.answerA.length != 0}>
        <div class="error">{errors.answerA}</div>
    </div>

    <div class="form-field">
        <label for="answer-b">Answer B: </label>
        <input type="text" id="answer-b" bind:value={fields.answerB} class:redBorder={errors.answerB.length != 0}>
        <div class="error">{errors.answerB}</div>
    </div>
    <Button type='secondary' flat={true}>Add Poll</Button>
</form>

<style>
    form{
        width: 400px;
        margin: 0 auto;
        text-align: center;
    }
    .form-field{
        margin: 18px auto;
    }
    input{
        width: 100%;
        border-radius: 6px;
    }
    label{
        margin: 10px auto;
        text-align: left;
    }
    .error{
        font-weight: bold;
        font-size: 12px;
        color: #d91b42;
    }
    .redBorder{
        border: 2px solid #d91b42;
    }

</style>