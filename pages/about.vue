<template>
  <div>
    <div id="nav">
      <Nav />
    </div>
    <div class="about">
      <b-jumbotron bg-variant="info" text-variant="white" border-variant="dark">
        <h1>About the Game:</h1>
        <h3>
          <ul>
            <li>Play 2 Win is a Quiz Game application that allows you to play quizzes with your friends and relatives in a simple and intuitive way.</li>
            <li>This is a multi-player quiz where many can participate to play the quiz game. Everyone will get different quiz adding it to their excitement.</li>
            <li>User can pay quickly with their account and play the quiz game. They can win the quiz and reward in HBAR which can be checked immediately in their account.</li>
            <li>If you do not have HBAR in your account, you can buy cryptocurrency online. We provided Moonpay to make it simpler to buy HBAR and play the game.</li>
          </ul>
        </h3>
      </b-jumbotron>
    </div>
  </div>
</template>

<script>
import Nav from "../components/Nav";

export default {
  components: {
    Nav
  }
};
</script>