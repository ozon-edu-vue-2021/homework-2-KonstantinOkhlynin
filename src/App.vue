<template>
  <div @click="(createPath($event))" class="root-container">
    <tree :tree-data="tree"></tree>
    <div class="info">{{`Путь: ${path}`}}</div>
  </div>
</template>

<script>
import Tree from "./components/Tree.vue";
import collections from "../public/static/node_modules.json";
export default {
  data: () => ({
    tree: collections,
    path: ''
  }),
  components: {
    Tree,
  },
    methods: {
    createPath: function (event) {
      if (event.target.classList.contains('name')) {
let current = event.target,
    list  = [],
    path = []
   while(current.parentNode != null && current.parentNode != document.documentElement) {
     list.push(current.parentNode);
     current = current.parentNode;
   }
   list.reverse()
   list.splice(0, 4);

   list.forEach((item)=> {
     if (item.classList.contains('node-tree')) {
path.push(item.children[0].textContent)
     }

   })
this.path = path.join('//')
      }
  },
  }
};
</script>
<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto+Slab&display=swap");
* {
  font-family: "Roboto Slab", serif;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  list-style: none;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-decoration: none;
  color: black;
}

html,body {
  height: 100%;
}

.root-container {
  background: #2c3e50;
  display: flex;
  height: 100%;
  width: 100%;
}

.info {
  padding: 1rem;
  display: flex;
  border-radius: 10px;
  box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.2);
  background: #fff;
  max-width: 500px;
  width: 100%;
  max-height: 101px;
  align-items: center;
}
</style>
