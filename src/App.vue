<template>
  <div v-if="showHome">
    <router-view />
  </div>
  <div v-else class="welcome">
    <h1>CREADOR DE PRESSUPOST WEB</h1>
    <div class="msgWelcome">
      <p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. Cumque perspiciatis vel quo cum odio impedit dignissimos eligendi nulla dolorem, beatae delectus ut. Obcaecati voluptate incidunt, distinctio earum illum odit facere doloremque labore sit sunt! Molestias, veniam nisi deleniti eius laudantium non ipsam sapiente omnis, qui, natus maxime? Adipisci, sed ullam?
      </p>
      </div>
  </div>
  <div class="swapBtn">
      <button v-if="!showHome" class="btnWelcome" @click="changeItems">ENTRA</button>
      <button v-else class="btnWelcome" @click="changeItems">TORNA A L'INICI</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showHome: false
    };
  },

  methods: {
    changeItems() {
      this.showHome = !this.showHome;
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@300;400;500;700&display=swap');

:root {
  --clr-1: #87baba; /*background color*/
  --clr-2: #2c3e50; /*text color*/
  --clr-3: #ff4a4a; /*unchecked*/
  --clr-4: #66ffba; /*checked*/
}

* {
  margin: 0;
  padding: 0;
  background-color: var(--clr-1);
  box-sizing: border-box;
}

h1 {
  font-size: 4.25rem;
}

#app {
  font-family: Oswald, Arial, sans-serif;
  text-align: center;
  color: var(--clr-2);
  margin: 2rem 0;
}

.welcome {
  margin: 3rem 2rem;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.msgWelcome {
  padding: 2rem;
  background-color: rgba(0, 0, 0, 0.15);
  border: solid rgb(255, 255, 255);
  border-radius: 25px;
  margin: 3rem 7rem;
}

.msgWelcome p {
  background-color: transparent;
  font-size: 1.2rem;
  font-weight: bold;
}

.btnWelcome {
  padding: .5rem;
  border-radius: 15px;
  border: solid rgba(255, 255, 255, 0.75);
  background-color: rgba(0, 0, 0, 0.15);
  color: white;
  font-size: 1.25rem;
  cursor: pointer;
  width: 12%;
  margin: 1rem 1.5rem;
}

.btnWelcome:active {
  transform: scale(0.96);
}

.btnWelcome:hover {
  background-color: rgba(0, 0, 0, 0.2);
}

</style>
