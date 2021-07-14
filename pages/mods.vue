<template>

  <div>
    <NavBar />
    <EditModModal :mod="selectedMod" />
    <DeleteModModal :mod="selectedMod" @onDeleted="getAll" />
    <div class="container">
      <h1>
        Mods
        <modEntryModal class="float-right" @onAdd="getAll" />
      </h1>
      <table class="table table-bordered tabled-striped">
        <thead>
          <tr class="bg-info text-white">
            <th>Brand</th>
            <th>Model</th>
            <th>Description</th>
            <th>Price</th>
            <th>Type</th>
            <th>&nbsp;</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="mod in mods" :key="mod.id">
            <td>{{mod.brand}}</td>
            <td>{{mod.model}}</td>
            <td>{{mod.description}}</td>
            <td>{{mod.value}}</td>
            <td>{{mod.type}}</td>
            <td>
              <b-button @click="onEdit(mod)" variant="info" size="sm">
                Edit
              </b-button>
              <b-button @click="onDelete(mod)" variant="danger" size="sm">
                Delete
              </b-button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>

</template>

<script>
export default {
  data() {
    return {
      mods: [],
      selectedMod: {}
    }
  },
  methods: {
    async getAll() {
      await this.$axios.get('/api/mods')
      .then((res)=>{
        if(res.status==200){
          this.mods = res.data
        }
      })
    },
    onEdit(selectedMod) {
      this.selectedMod = selectedMod
      this.$bvModal.show('editModModal')
    },
    onDelete(selectedMod) {
      this.selectedMod = selectedMod
      this.$bvModal.show('deleteModModal')
    }
  },
  created() {
    this.getAll()
  }
}

</script>

<style>

</style>
