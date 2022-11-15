<template>
    <form class="arrowContainer">
      <button class="button" type="button" @click="decrease"><fa class="arrowIcon iconMinus" icon="fa-solid fa-circle-arrow-down" /></button>
      <input class="input" type="number" v-model="quantity" />
      <button class="button" type="button" @click="increase"><fa class="arrowIcon iconPlus" icon="fa-solid fa-circle-arrow-up" /></button>
    </form>
  </template>
  
  <script>
  export default {
    name: "ContadorItem",
    emits: ["changeQuantity"],
    data() {
      return {
        quantity: 1,
      };
    },
    methods: {
      decrease() {
        this.quantity > 1 ? this.quantity-- : (this.quantity = 1);
      },
      increase() {
        this.quantity < 1 ? (this.quantity = 1) : this.quantity++;
      },
      emitQuantity() {
        this.$emit("changeQuantity", this.quantity);
      },
    },
    watch: {
      //Sempre > 0
      quantity() {
        if (this.quantity >= 1) {
          this.emitQuantity();
        } else {
          alert("Només números positius.");
        }
      },
    },
  };
</script>
  
<style scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
  
.input {
  width: 4rem;
  text-align: center;
  padding: 5px;
  border: none;
  background: transparent;
  font-weight: 900;
  font-size: 16px;
  border-radius: 4px;
  color: white;
  margin: 0 10px;
}

.arrowContainer {
  width: 50%;
  margin: 10px auto;
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.15);
  border-radius: 30px;
  }
  
.button {
  border: none;
  cursor: pointer;
  background: transparent;
}

.button:active {
  transform: scale(0.94);
}

.arrowIcon {
  font-size: 1.8rem;
  border-radius: 100%;
  background-color: var(--clr-2);
}

.iconPlus {
  color: var(--clr-4);
}
.iconMinus {
  color: var(--clr-3);
}
</style>
  