<template>
  <div v-if="showWebOptions" id="webOptions">
    Número de pàgines
    <fa icon="fa-solid fa-circle-info" class="infoButton" data-bs-toggle="modal" data-bs-target="#pgModal" />
      <ContadorItem @changeQuantity="changePag" />
    Número d'idiomes
    <fa icon="fa-solid fa-circle-info" class="infoButton" data-bs-toggle="modal" data-bs-target="#lgModal" />
      <ContadorItem @changeQuantity="changeLang" />
  </div>
  <div class="modal" id="pgModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-body">Cal especificar el número de pàgines de què constarà el lloc web.</div>
      </div>
    </div>
  </div>
  <div class="modal" id="lgModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-body">Cal especificar el número d'idiomes de què constarà el lloc web.</div>
      </div>
    </div>
  </div>
</template>

<script>
import ContadorItem from "./ContadorItem.vue";

export default {
  name: "PanellItem",
  emits: ["changePag", "changeLang"],
  components: { ContadorItem },
  props: [],
  data() {
    return {
      showWebOptions: true,
    };
  },
  methods: {
    changePag(value) {
      this.$emit("changePag", value);
    },
    changeLang(value) {
      this.$emit("changeLang", value);
    },
  },
}
</script>

<style scoped>
#webOptions {
  border: 1px solid rgb(0, 0, 0);
  padding: 1rem;
  width: 30%;
  border-radius: 15px;
}

.infoButton {
  cursor: pointer;
}

.modal, .modal-dialog{
  background-color: transparent;
  border: none;
}

.modal-content { 
  width: 100%;
  padding: .1em;
  margin-top: 14vh;
  margin-left: auto;
  margin-right: auto;
  border-radius: 20px;
  background-color: var(--clr-2);
}

.modal-body {
  color: var(--clr-2);
  border-radius: .8px;
  box-shadow: none;
  padding: 2rem;
  font-size: 1.8rem;
  border-radius: 20px;
}
</style>
