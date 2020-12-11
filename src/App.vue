<template>
  <div id="app">
    <navbar />
    <router-view/>
  </div>
</template>

<script>
import Navbar from '@/components/Header/Navbar'

export default {
  components: { Navbar }
}
</script>