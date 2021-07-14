<template>
  <div>

    <b-modal id="editModModal" title="Mod Entry" ok-title="Save Mod" @ok="onSubmit">
      <form action="#">
        <b-form-group
          label="Brand"
          label-for="brand"
        >
          <b-form-input id="brand" v-model="mod.brand" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Model"
          label-for="model"
        >
          <b-form-input id="model" v-model="mod.model" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Description"
          label-for="description"
        >
          <b-form-input id="description" v-model="mod.description" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Value"
          label-for="value"
        >
          <b-form-input id="value" v-model="mod.value" trim></b-form-input>
        </b-form-group>

        <b-form-group
          label="Type"
          label-for="type"
        >
          <b-form-select v-model="mod.type" :options="types"></b-form-select>
        </b-form-group>

      </form>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    mod: {}
  },
  data() {
    return {
      types: [
        {value: 'variable', text: 'Variable'},
        {value: 'mechanical', text: 'Mechanical'},
      ]
    }
  },
  methods: {
    async onSubmit() {
      this.$axios.put('/api/mods/' + this.mod.id, this.mod)
      .then((res)=>{
        if(res.status==202) {
          alert('Update successful!')
        }
      })
      .catch((err)=>{
        alert(err.message)
      })
    }
  }
}
</script>
