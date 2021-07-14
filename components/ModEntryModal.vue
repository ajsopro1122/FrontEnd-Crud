<template>
  <div>
    <b-button v-b-modal.modEntryModal variant="primary">Add Mod</b-button>
    <b-modal id="modEntryModal" title="Mod Entry" ok-title="Save Mod" @ok="onSubmit">
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
  data() {
    return {
      mod: {},
      types: [
        {value: 'variable', text: 'Variable'},
        {value: 'mechanical', text: 'Mechanical'},
      ]
    }
  },
  methods: {
    async onSubmit() {
      this.$axios.post('/api/mods', this.mod)
      .then((res)=>{
        if(res.status==202) {
          alert('Successfully added the mod')
          this.$emit('onAdd')
          this.mod = {}
        }
      })
    }
  }
}
</script>
