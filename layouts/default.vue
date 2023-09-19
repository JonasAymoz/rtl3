<template>
    
    <div class=" layout__container">
        <Header></Header>
        <slot />
    </div>
</template>

<script>
import Header from '../components/Header.vue'
    export default {
  components: { Header },
        
    }
</script>

<style lang="postcss" scoped>
.layout__container {
    height : 100vh;
}
</style>