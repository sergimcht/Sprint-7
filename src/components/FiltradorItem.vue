<template>
    <div>
        <button @click="sortName">Ordena per Nom</button>
        <button @click="sortDate">Ordena per Data</button>
        <button @click="sortReset">Reinicia Ordre</button>
    </div>
    <div class="search">
        <label for="search">Nom del Projecte:</label>
        <input type="text" id="search" v-model="budgetSearch">
        <button @click="searchBudget">Busca Projecte</button>
    </div>
    <h3>PRESSUPOSTOS GUARDATS</h3>
    <div v-for="item, index in selectedArray" :key="index">
        <div v-if="item.total > 0">
        <div class="savedBudget">
            <p>Nom Client: {{ item.name }}</p>
            <p>Nom Projecte: {{ item.project }}</p>
            <p class="total">Total: {{ item.total }}€</p>
        </div>
        </div>
    </div>
</template>
  
  <script>
  export default {
    name: "FiltradorItem",
    props: ["budgetList"],
    data() {
        return {
            budgetArray: this.budgetList,
            arrayFiltered: [],
            selectedArray: this.budgetList,
            budgetSearch: ""
        }
    },
    methods: {
    sortName() {
        this.selectedArray = this.budgetArray
        this.budgetArray.sort((a, b) => a.name.localeCompare(b.name))
    },
    sortDate() {
        this.selectedArray = this.budgetArray
        this.budgetArray.sort((a, b) => (a.date).toString().localeCompare(b.date.toString()))
    },
    sortReset() {
        this.sortDate();
    },
    searchBudget() {
        if (this.budgetSearch.length > 0 && isNaN(this.budgetSearch)) {
            this.arrayFiltered = []
            this.arrayFiltered.push(this.budgetArray.find(item => item.project.includes((this.budgetSearch).toUpperCase())))
            this.selectedArray = this.arrayFiltered
        } else {
            alert("El camp de cerca no pot contenir números ni estar buit.")
        }
        this.budgetSearch = ""
    },
  },
};
</script>

<style scoped>
* {
    margin: 0;
}

.savedBudget {
    margin: 2rem auto;
    box-shadow: 1px 2px 4px 3px rgba(0, 0, 0, 0.6);
    padding: 1rem 0;
    width: 40%;
    border-radius: 5px;
    color: white;
    background-color: rgba(0, 0, 0, 0.15);
}

.savedBudget p {
    background-color: transparent;
}

.total {
    font-weight: bold;
}

h3 {
    margin: 10px 0 0 0;
    color: var(--clr-2)
}

button {
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

button:active {
    transform: scale(0.96);
}

button:hover {
    background-color: rgba(0, 0, 0, 0.2);
}

input {
    border-radius: 5px;
    border: solid rgba(255, 255, 255, 0.75);
    background: rgba(0, 0, 0, 0.15);
    text-align: center;
    padding: 5px;
    color: white;
}

.search label {
    color: var(--clr-2);
    font-size: 1.4rem;
    margin: 0 1.6rem;
}
</style>
  