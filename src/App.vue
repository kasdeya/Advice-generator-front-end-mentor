<script lang="ts">
export default {
  data() {
    return {
      result: {
        id: '',
        advice: '',
      },
      responseAvailable: false,
    }
  },
  methods: {
    fetchAPIData() {
      // fetch("https://api.adviceslip.com/advice")
      fetch(`https://api.adviceslip.com/advice?_=${new Date().getTime()}`)
        .then(response => {
          if (response.ok) {
            return response.json();
          } else {
            console.log("Server returned " + response.status + " :" + response.statusText)
          }
        })
        .then(data => {
          this.result.id = data.slip.id
          this.result.advice = data.slip.advice
          console.log(this.result.advice)
        })
    },
  },
  mounted() {
    this.fetchAPIData();
  },
}
</script>

<template>
  <main>
    <div class="card">
    <h2>
      ADVICE #{{ result.id }}
    </h2>
    <p>
    "{{ result.advice }}"
    </p>
    <img src="./assets/images/pattern-divider-desktop.svg" class="img1">
    <img src="./assets/images/pattern-divider-mobile.svg" class="img2">
    <button @click="fetchAPIData"><img src="./assets/images/icon-dice.svg"></button>
    </div>
  </main>
</template>

<style scoped>

.card {
  position: relative;
  background-color: var(--dark-grayish-blue);
  color: var(--light-cyan);
  font-size: 28px;
  text-align: center;
  padding: 3rem;
  width: 600px;
  margin: auto;
  border-radius: 12px;
}
.card h2 {
  color: var(--neon-green);
  font-size: 13px;
  letter-spacing: 4px;
  margin-bottom: 1rem;
}

.card p {
  margin-bottom: 1rem;
}

.card button {
  background-color: var(--neon-green);
  border-radius: 100px;
  outline: transparent;
  border: transparent;
  padding: 1rem;
  position: absolute;
  bottom: -32px;
  cursor: pointer;
  left: 0;
  right: 0;
  margin: auto;
  width: fit-content;
}

.card button:hover {
  box-shadow: 0px 0px 45px -5px var(--neon-green);
}

.img1 {
  width: 100%;
}

.img2 {
  display: none;
}

@media (max-width: 650px) {
  .card {
    width: 90%;
  }
  .img1 {
    margin: auto;
    display:none;
  }

  .img2 {
    margin: auto;
    width: 100%;
    display: block;
  }
}
</style>
