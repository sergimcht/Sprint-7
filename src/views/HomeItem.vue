<template>
  <div id="selectOptions">
    <h1>QUÈ VOLS FER?</h1><br>
    <div class="options">
      <label for="web">Una pàgina web (500€)</label><br>
      <input type="checkbox" id="web" :value=500 v-model="checkedPrices" @change="calculatePrice">
    </div>
    <div class="panel" v-if=checkedPrices.includes(500)>
      <PanellItem @changePag="changePag" @changeLang="changeLang"/>
    </div>
    <div class="options">
      <label for="seo">Una consultoria SEO (300€)</label><br>
      <input type="checkbox" id="seo" :value=300 v-model="checkedPrices" @change="calculatePrice">
    </div>
    <div class="options">
      <label for="ads">Un campanya de Google Ads (200€)</label><br>
      <input type="checkbox" id="ads" :value=200 v-model="checkedPrices" @change="calculatePrice">
    </div>
    <p class="total">PREU: {{ totalPrice }}€</p>
  </div>
  <div class="budgetInfo">
    <label class="budgetLabel" for="clientName">El teu nom: </label>
    <input type="text" id="clientName" v-model="userName" />
    <label class="budgetLabel" for="project">Nom del projecte: </label>
    <input type="text" id="projectName" v-model="projectName" />
  </div>
  <button class="button" type="button" @click="handleSubmit">ENVIA</button>
  <FiltradorItem v-if="budgetList.length" :budgetList="budgetList"/>
</template>

<script>
import PanellItem from "../components/PanellItem.vue";
import FiltradorItem from "../components/FiltradorItem.vue";

export default {
  name: "HomeItem",
  components: { PanellItem, FiltradorItem },
  props: [],
  data() {
    return {
      checkedPrices: [],
      totalPrice: 0,
      costLangPage: 30,
      nPag: 1,
      nLang: 1,
      budgetList: [ //BBDD pre-carregada per provar funcionalitats
        {
          name: "AA",
          project: "AA",
          total: 300,
          date: 1668460992352,
        },
        {
          name: "CC",
          project: "CC",
          total: 1200,
          date: 1668460992365,
        },
        {
          name: "BB",
          project: "BB",
          total: 3200,
          date: 1668460992389,
        }
      ],
      userName: "",
      projectName: ""
    }
  },
  methods: {
    calculatePrice() {
      this.totalPrice = 0;
      this.totalPrice += this.checkedPrices.reduce((a, b) => a + b, 0);
      if (this.checkedPrices.includes(500)) {
        this.totalPrice += (this.nPag * this.nLang * this.costLangPage);
      } else {
        this.nPag = 1;
        this.nLang = 1;
      }
    },
    changePag(value) {
      this.nPag = value;
      this.calculatePrice();
    },
    changeLang(value) {
      this.nLang = value;
      this.calculatePrice();
    },
    handleSubmit() {
      if (this.userName.length > 0 && this.projectName.length > 0 && isNaN(this.userName) && isNaN(this.projectName)) {
        if (this.totalPrice > 0) {
          this.budgetList.push({
            name: (this.userName).toUpperCase(),
            project: (this.projectName).toUpperCase(),
            total: this.totalPrice,
            date: Date.now()
          });
        }
      } else {
        alert("El camp pel teu nom i el del projecte no pot contenir números ni estar buit.");
      }
      this.userName = "";
      this.projectName = "";
    },
  }
}
</script>

<style scoped>
.total {
  font-size: 3rem;
  margin: -1rem 0 1.5rem 0;
}

label {
  font-size: 1.5rem;
  background-color: transparent;
}

.panel {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 80rem;
}

#selectOptions {
  display: flex;
  align-items: center;
  flex-direction: column;
}

.options {
  margin: 1.5rem 0;
  width: 60rem;
  background: #00000020;
  color: white;
  padding: 15px;
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
}

input[type="checkbox"] {
  cursor: pointer;
  position: relative;
  width: 65px;
  height: 30px;
  appearance: none;
  background: var(--clr-3);
  outline: none;
  border-radius: 7.5px;
  transition: 0.7s;
  box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
  margin: 0 10px;
}

input:checked[type="checkbox"] {
  background: var(--clr-4);
}

input[type="checkbox"]:before {
  content: "";
  position: absolute;
  width: 30px;
  height: 30px;
  border-radius: 5px;
  top: 0;
  left: 0;
  background: #fff;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.35);
  transition: 0.3s;
}

input:checked[type="checkbox"]:before {
  left: 35px;
}

input[type="text"] {
  border-radius: 5px;
  border: solid rgba(255, 255, 255, 0.75);
  background: rgba(0, 0, 0, 0.15);
  text-align: center;
  padding: 5px;
  color: white;
}

.budgetLabel {
  font-size: 1.4rem;
  margin: 0 30px;
}

.budgetInfo {
  margin: auto;
  background: #00000020;
  color: white;
  padding: 15px;
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: row;
  width: 60rem;
}

button {
  padding: .5rem;
  border-radius: 15px;
  border: solid rgba(255, 255, 255, 0.75);
  background-color: rgba(0, 0, 0, 0.15);
  font-weight: bold;
  color: white;
  font-size: 1.75rem;
  cursor: pointer;
  width: 12rem;
  margin: 1.5rem 0;
}

button:active {
  transform: scale(0.96);
}

button:hover {
  background-color: rgba(0, 0, 0, 0.2);
}
</style>
