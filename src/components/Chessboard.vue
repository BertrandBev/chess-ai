<template lang='pug'>
//- chessboard
v-layout(row justify-center style='margin-top: 120px')
  .cg-board-wrap(ref='chessground')
</template>

<script>
import { chessboard } from "vue-chessboard";
import { Chessground } from "chessground";
import Chess from "chess.js";

export default {
  name: "Chessboard",

  components: {
    chessboard
  },

  props: {},

  data: () => ({
    state: null,
    board: null
  }),

  computed: {},

  methods: {
    toColor() {
      return this.state.turn() === "w" ? "white" : "black";
    },

    possibleMoves() {
      const dests = {};
      this.state.SQUARES.forEach(s => {
        const ms = this.state.moves({ square: s, verbose: true });
        if (ms.length) dests[s] = ms.map(m => m.to);
      });
      return dests;
    },

    reset() {
      this.state.reset();
      this.board = Chessground(this.$refs.chessground, {
        fen: this.state.fen(),
        turnColor: this.toColor(),
        movable: {
          color: this.toColor(),
          free: true,
          dests: this.possibleMoves()
        },
        orientation: "white"
      });
      console.log("board fen", this.board.getFen());
      this.board.set({
        movable: { events: { after: this.changeTurn } }
      });
    },

    changeTurn(orig, dest, metadata) {
      this.state.move({ from: orig, to: dest, promotion: "q" });
      this.board.set({
        fen: this.state.fen(),
        turnColor: this.toColor(),
        movable: {
          color: this.toColor(),
          dests: this.possibleMoves()
        }
      });
    }
  },

  created() {
    this.state = new Chess();
  },

  mounted() {
    this.reset();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style src='./style/theme.css'>
</style>