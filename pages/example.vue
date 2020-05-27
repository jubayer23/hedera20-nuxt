<template>
  <div class="container">
    <div>
      <h1 class="title">
        hedera20
      </h1>
      <h2 class="subtitle">
        Web Quiz app
      </h2>
      <div class="links">
        <a
          href="/quiz"
          target=""
          class="button--green"
          @click.prevent="iniAcc"
        >
          Win 500ħ
        </a>
        <a
          href="/quiz"
          target=""
          class="button--grey"
        >
          Win 1000ħ
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  components: {
  },
  methods: {
    iniAcc () {
      const msg = {
        message: "connected"
      }
      console.log(msg)
      axios.post('http://localhost:5000/hedera/send', msg)
      .then(res => {
        console.log(res.data)
        if(res.data == 'amount sent') {
          window.location = '/quiz'
        } 
        else {
          alert('tx problem')
        }
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

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
