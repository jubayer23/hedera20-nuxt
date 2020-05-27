<template>
    <div class="result">
        <h1>You Scored {{numCorrect}} out of {{numTotal}}</h1>
        <b-button size="lg" variant="primary" to="/">Play Again</b-button>
    </div>
</template>

<script>

import axios from 'axios';

export default {
    props: [
        'numCorrect',
        'numTotal'
    ],
    mounted: function() {
        if(this.numCorrect === this.numTotal) {
            alert("You Won")
            const message = {
                account: localStorage.account
            }
            console.log(message)
            axios.post('http://localhost:5000/hedera/fiveh', message)
            .then(res => {
                
            })
            .catch(
                err => {
                console.error(err)
                }
            );
        }
  }
}
</script>