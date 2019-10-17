<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <Chessboard/>
  </div>
</template>

<script>
// @ is an alias to /src
import Chessboard from '@/components/Chessboard.vue'

export default {
  name: 'home',
  components: {
    Chessboard
  }
}
</script>
