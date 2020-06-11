<template>
  <div>
    <div id="nav">
      <Nav />
    </div>
    <div class="how">
      <b-jumbotron bg-variant="success" text-variant="white" border-variant="dark">
        <h1>How TO Play The Game:</h1>
        <h2>
          <ol>
            <li>Login to Hedera Account with your credentials.</li>
            <li>Select the Quiz Game to play.</li>
            <ul>
              <li>There are 2 Quiz Games with different prizes to win.</li>
              <li>There are different fees to play each Quiz.</li>
            </ul>
            <li>Answer all the Quiz questions correctly to win the prize.</li>
            <li>You fail in winning the quiz-Never loose faith and try again</li>
            <li>You succeed in winning the quiz and receive the reward according to the quiz you played. Enjoy your winning by spending your money in HBAR!</li>
          </ol>
        </h2>
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