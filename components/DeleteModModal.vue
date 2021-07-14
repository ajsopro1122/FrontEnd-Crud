<template>
  <div>

    <b-modal id="deleteModModal" title="Mod Entry" ok-title="Delete Mod" @ok="onDelete" ok-variant="danger">
      Are you sure about deleting this mod? <br>
      {{ mod.brand }} {{ mod.description }}
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    mod: {}
  },
  methods: {
    async onDelete() {
      this.$axios.delete('/api/mods/' + this.mod.id)
      .then((res)=>{
        if(res.status==202) {
          alert('Mod is deleted successfully!')
          this.$emit('onDeleted')
        }
      })
    }
  }
}
</script>
