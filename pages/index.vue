<template>
<div class="content">
  <div id="nav">
    <Nav />
  </div>
  <div class="main">
    <div id="art">
      <h1>Play 2 Win</h1>
      <h1>Quiz</h1>
    </div>
    <div class="cent">
      <div class="left">
        <b-button size="lg" variant="outline-primary" @click="five">Win 500ħ</b-button>
        <h3>Entry Fee 5ħ</h3>
      </div>
      <div class="right">
        <b-button size="lg" variant="outline-primary" @click="ten">Win 1000ħ</b-button>
        <h3>Entry Fee 10ħ</h3>
      </div>
    </div>
    <div class="account">
        <div>
          <b-button id="show-btn" @click="$bvModal.show('bv-modal-example')">Load Account</b-button>

          <b-modal id="bv-modal-example" title="Load Your Hedera Account" hide-footer>
            <b-form-group label="Account Id" label-for="dropdown-form-email" @submit.stop.prevent>
              <b-form-input
                id="dropdown-form-email"
                size="sm"
                placeholder="0.0.****"
                v-model="account"
              ></b-form-input>
            </b-form-group>

            <b-form-group label="Private Key" label-for="dropdown-form-password">
              <b-form-input
                id="dropdown-form-password"
                type="password"
                size="sm"
                v-model="pk"
                placeholder="private key"
              ></b-form-input>
            </b-form-group>

            <b-button class="mt-3" block @click="onClickLock">Load</b-button>
          </b-modal>
        </div>
      <h3>Your account current balance</h3>
      <h2>{{bal}} ħ</h2>
      <p>
        <a href="https://buy.moonpay.io/hbar">click here</a> to get some HBAR into your hedera wallet
      </p>
    </div>
  </div>
</div>    
</template>

<script>
import Nav from '../components/Nav';

import axios from 'axios';

export default {
    components: {
    Nav
  },
   data() {
    return {
      bal:0,
      account:'',
      pk:''
    }
  },
  /*created: function() {
      window.addEventListener('beforeunload', function(event) {
        localStorage.clear();
        event.returnValue = 'something';
      })
    },*/
    mounted() {
    {
      if (localStorage.account && localStorage.pk) {
        console.log("mounted");
        const info = {
          account: localStorage.account,
          pk: localStorage.pk
        };
        axios
          .post("http://localhost:5000/hedera/bal", info)
          .then(res => {
            console.log(res.data);
            this.bal = res.data;
          })
          .catch(err => {
            console.error(err);
          });
      }
    }
  },
   methods: {
     onClickLock() {
        localStorage.account = this.account;
      localStorage.pk = this.pk;
      if (localStorage.account && localStorage.pk) {
        console.log("account loaded");
        const info = {
          account: localStorage.account,
          pk: localStorage.pk
        };
        axios
          .post("http://localhost:5000/hedera/bal", info)
          .then(res => {
            console.log(res.data);
            this.bal = res.data;
          })
          .catch(err => {
            console.error(err);
          });
      }
      this.$bvModal.hide("bv-modal-example");
      },
      onClickUnlock() {
        localStorage.clear();
        this.$bvModal.hide("bv-modal-example");
      },
    five () {
      if(localStorage.account) {
        const info = {
          account: localStorage.account,
          pk: localStorage.pk
        }
        axios.post('https://floating-basin-51607.herokuapp.com/hedera/five', info)
        .then(res => {
          if(res.data.status == 'SUCCESS') {
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
      else {
        alert("Please Load Your Account Details To Play")
      }
    },
    ten () {
      if(localStorage.account) {
        const info = {
          account: localStorage.account,
          pk: localStorage.pk
        }
        axios.post('https://floating-basin-51607.herokuapp.com/hedera/ten', info)
        .then(res => {
          if(res.data.status == 'SUCCESS') {
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
      else {
        alert("Please Load Your Account Details To Play")
      }
    }
  }
}
</script>

<style scoped>
.content {
  background-color: blanchedalmond;
}
.main {
  margin: auto;
  width:50%;
  text-align: center;
  padding: 10px;
}
.cent {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  position: relative;
  top: 50px;
}
.account {
  position: relative;
  top: 200px;
}
h2 {
  border: 3px solid green;
}
</style>
