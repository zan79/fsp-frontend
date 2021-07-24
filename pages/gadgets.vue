<template>
  <div>
    <NavBar/>
    <div class="container mt-5">
      <h1 class="text-warning">Gadgets</h1>
      <hr class="bg-warning">
      <div class="row">
        <div class="col-6">
          <h5 class="text-light">List of Gadgets</h5>
          <ul class="list-group">
            <li class="list-group-item list-group-item-action" v-for="gadget in gadgets" :key="gadget.id" @click="onSelected(gadget)">
              {{gadget.name}} <span class="float-right">{{gadget.price}}</span>
            </li>
          </ul>
        </div>
        <div class="col-6">
          <GadgetView :gadget="selectedGadget" @saveGadget="onChanges" @newGadget="onNewGadget" @deleteGadget="onChanges"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      gadgets: [],
      selectedGadget: {}
    }
  },
  methods: {
    async getGadgets(){
      await this.$axios.get('/api/gadgets')
      .then((res)=>{
        if(res.status==200){
          this.gadgets = res.data
        }
      })
    },
    onNewGadget(){
      this.selectedGadget = {}
    },
    onChanges(){
      this.getGadgets()
      this.selectedGadget = {}
    },
    onSelected(gadget){
      this.selectedGadget = gadget 
    }
  },
  created() {
    this.getGadgets()
  }
}
</script>

<style>
body{
  background-color: #212121;
}
</style>