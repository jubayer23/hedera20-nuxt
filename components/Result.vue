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
            if (this.$route.params.amt === "five") {
                axios.post('https://floating-basin-51607.herokuapp.com/hedera/fiveh', message)
                .then(res => {

                })
                .catch(
                    err => {
                    console.error(err)
                    }
                );
            } else {
            
                axios.post('https://floating-basin-51607.herokuapp.com/hedera/tenh', message)
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
}
</script>
