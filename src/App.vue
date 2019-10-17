<template lang='pug'>
v-app
  v-app-bar(app='')
    v-toolbar-title.headline.text-uppercase
      span Chess
      span.ml-2.font-weight-light playground
    v-spacer
    v-btn(text='' href='https://github.com/vuetifyjs/vuetify/releases/latest' target='_blank')
      span.mr-2 Latest Release
  v-content
    Chessboard
</template>

<script>
import Chessboard from './components/Chessboard';

export default {
  name: 'App',
  components: {
    Chessboard,
  },
  data: () => ({
    //
  }),
};
</script>
