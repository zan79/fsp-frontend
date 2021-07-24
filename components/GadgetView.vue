<template>
  <div>
    <button class="btn btn-success float-right" @click="onNew">
      New Gadget
    </button>
    <h5 class="text-light">Gadget View</h5>
    <hr class="bg-light">

    <form class="text-light" action="" @submit.prevent="">
      <div class="row">

        <div class="col-6">
          <b-form-group label="Name">
            <b-form-input v-model="gadget.name"></b-form-input>
          </b-form-group>

          <b-form-group label="Brand">
            <b-form-input v-model="gadget.brand"></b-form-input>
          </b-form-group>

          <b-form-group label="Description">
            <b-form-input v-model="gadget.description"></b-form-input>
          </b-form-group>
        </div>

        <div class="col-6">
          <b-form-group label="Price">
            <b-form-input type="number" v-model="gadget.price"></b-form-input>
          </b-form-group>

          <b-form-group label="Stock">
            <b-form-input type="number" v-model="gadget.stock"></b-form-input>
          </b-form-group>

          <b-form-group label="Date Acquired">
            <b-form-input type="date" v-model="gadget.acquired_on"></b-form-input>
          </b-form-group>
        </div>
        
      </div>

      <b-form-group>
        <button class="btn btn-primary" @click="onSave">Save Changes</button>
        <button class="btn btn-danger" @click="onDelete" v-if="gadget.id">Delete</button>
      </b-form-group>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    gadget: {}
  },
  methods: {
    async onSave(){
      try {
        if(!this.gadget.id){
          await this.$axios.post('/api/gadgets', this.gadget)
          //alert('Add gadget successful')
        }else{
          await this.$axios.put('/api/gadgets/' + this.gadget.id, this.gadget)
          //alert('Update gadget successful')
        }

        this.$emit('saveGadget')
      }catch(err) {
        alert(err.response.data.message)
      }
    },
    onNew(){
      this.$emit('newGadget')
    },
    async onDelete(){
      try{
        this.$axios.delete('/api/gadgets/' + this.gadget.id)
        this.$emit('deleteGadget')
      }catch(err){
        alert(err.response.data.message)
      }
    }
  }
}
</script>

<style>
body{
  background-color: #212121;
}
</style>