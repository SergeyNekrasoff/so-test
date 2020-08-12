<template>
  <div id="app">
    <tree :list="list" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Tree from './components/Tree.vue';

@Component({
  components: {
    tree: Tree,
  }
})

export default class App extends Vue {
  list: Array<object> = [];

  constructor() {
    super();
    this.list = [{
      id: 1,
      parentId: 0,
      name: 'Редактировать пользователя',
      checked: true
    },
    {
      id: 2,
      parentId: 1,
      name: 'Удалить пользователя',
      checked: true
    },
    {
      id: 3,
      parentId: 2,
      name: 'Остановить пользователя',
      checked: false
    },
    {
      id: 4,
      parentId: 3,
      name: 'Скрыть пользователя',
      checked: false
    }];
  }
}
</script>

<style lang="scss">
@import "assets/main";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
