<template>
  <div>

    <b-modal id="deleteAssetModal" title="Asset Entry" ok-title="Delete Asset" @ok="onDelete" ok-variant="danger">
      Are you sure about deleting this asset? <br>
      {{ asset.name }} {{ asset.description }}
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    asset: {}
  },
  methods: {
    async onDelete() {
      this.axios.delete('/api/assets/' + this.asset.id)
      .then((res)=>{
        if(res.status==202) {
          alert('Asset is deleted successfully!')
          this.$emit('onDeleted')
        }
      })
    }
  }
}
</script>
