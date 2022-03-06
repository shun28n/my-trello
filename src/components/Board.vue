<template>
  <div>
    <header>my Trello</header>
    <main>
      <p class="info-line">All: {{ totalCardCount }}tasks</p>
      <draggable class="list-index" :list="lists" @end="movingLists">
        <list
          v-for="(item, index) in lists"
          :key="item.id"
          :title="item.title"
          :listIndex="index"
          :cards="item.cards"
          @change="movingCards"
        />
        <list-add />
      </draggable>
    </main>
  </div>
</template>

<script>
import List from "./List.vue";
import ListAdd from "./ListAdd.vue";
import { mapState } from "vuex";
import draggable from "vuedraggable";

export default {
  components: {
    ListAdd,
    List,
    draggable,
  },
  computed: {
    // mapState: storeのstateで定義した同じ名前で呼び出せる
    ...mapState(["lists"]),
    totalCardCount() {
      // stateのlistsを算出したものを返す。stateの算出はgetters
      return this.$store.getters.totalCardCount;
    },
  },
  methods: {
    movingCards: function () {
      this.$store.dispatch("updateList", { lists: this.lists });
    },
    movingLists: function () {
      this.$store.dispatch("updateList", { lists: this.lists });
    },
  },
};
</script>

<style>
</style>