<template>
  <div class="container">
    <router-link :to=" '/viaje/' + id">
      <div class="card">
        <div class="card-top">
          <h3>{{ nombre }} | {{ destino }}</h3>
          <span>({{ carrera }})</span>
        </div>
        <div class="card-description">
          <span>{{ descripcionCorta }}</span>
        </div>
      </div>
    </router-link>
    <div class="btn-eliminar" v-on:click="deleteViaje()">
      <font-awesome-icon icon="trash" />
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "TarjetaViaje",
  props: {
    nombre: String,
    destino: String,
    carrera: String,
    descripcionCorta: String,
    id: Number
  },
  methods: {
    deleteViaje() {
      axios.delete("http://127.0.0.1:8000/api/viajes/" + this.id).then(res => {
        if (res.status == "200") {
          this.$parent.getViajes();
        }
      });
    }
  }
};
</script>

<style lang="stylus" scoped>

  h3
    margin 0 10px 0 0

  .container
    margin-bottom 10px
    cursor pointer
    
    a
    &:hover
      text-decoration none

  .card
    display flex
    box-shadow 0 5px 3px -3px rgba(0,0,0,.0)
    transition .5s
    &:hover
      box-shadow 0 5px 3px -3px rgba(0,0,0,.3)

  .card-top
    display flex
    flex-direction row
    align-items center
    padding 10px

  .card-description
    margin 0 0 10px 10px
    color #555

  .btn-eliminar
    position relative
    float right
    margin-top -65px
    margin-right 10px
    padding 15px

    &:hover
      color red

</style>
