<template>
  <div>
    <div v-if="showNav">
      <AppNav></AppNav>
    </div>
    <router-view/>
  </div>
</template>
<script>
import AppNav from "@/components/AppNav.vue"
export default {
  components: {
    AppNav
  },
  data (){
    return {
      // showNav:false,
    }
  },
  computed:{
    showNav(){
      return (this.$route.name==='login') ? false: true 
    }
  },
}
</script>
