<template>

      <div id="part">
        <img :src="partData.image" alt="part" />
      </div>

</template>

<script>
    export default {
        name:"Part",
        props:{
            partData:{
                type:Object,
                default:{}
            }
        }
        
    }
</script>

<style lang="scss" scoped>

</style>