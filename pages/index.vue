<template>
<div class="content">
  <div id="nav">
    <Nav />
  </div>
  <div class="main">
    <div id="art">
      <h1>Play to Win</h1>
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
          <b-dropdown id="dropdown-form" text="Account Credentials" ref="dropdown" class="l-2">
            <b-dropdown-form>
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

              <b-button variant="primary" size="sm" @click="onClickLock">Lock</b-button>
              <b-button variant="danger" size="sm" @click="onClickUnlock">Unlock</b-button>
              <b-dropdown-divider></b-dropdown-divider>
              <p><a href="https://buy.moonpay.io/hbar">click here </a>to get some HBAR into your hedera wallet</p>
            </b-dropdown-form>
            <b-dropdown-divider></b-dropdown-divider>
          </b-dropdown>
        </div>
      <h3>Your account current balance</h3>
      <h2>{{bal}} ħ</h2>
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
   methods: {
     onClickLock() {
        localStorage.account=this.account;
        localStorage.pk=this.pk;
        this.$refs.dropdown.hide(true)
      },
      onClickUnlock() {
        localStorage.clear();
        this.$refs.dropdown.hide(true)
      },
    five () {
      if(localStorage.account) {
        const info = {
          account: localStorage.account,
          pk: localStorage.pk
        }
        axios.post('http://localhost:5000/hedera/five', info)
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
        alert("Please Enter Your Account Details To Play")
      }
    },
    ten () {
      if(localStorage.account) {
        const info = {
          account: localStorage.account,
          pk: localStorage.pk
        }
        axios.post('http://localhost:5000/hedera/ten', info)
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
        alert("Please Enter Your Account Details To Play")
      }
    }
  },
  watch: {
    account : function(){
      if(localStorage.account) {
        const info = {
          account: localStorage.account,
          pk: localStorage.pk
        }
      axios.post('http://localhost:5000/hedera/bal',info)
      .then(res => {
          console.log(res.data);
          this.bal = res.data;
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
  top: 150px;
}
h2 {
  border: 3px solid green;
}
</style>
