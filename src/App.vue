<template>
  <div @click="(createPath($event))"  class="root-container">
    <tree :tree-data="tree"></tree>
    <div class="card">
    <div class="info"> <h1 class="path">{{`Путь: ${path}`}}</h1></div>
    <div class="info"> 
      <h1 class="navigations">Клавиатурная навигация</h1>
      <p class="text"><span class="text-button">Enter</span> открыть/закрыть папку</p>
      <p class="text"><span class="text-button">TAB</span> перемещаться по списку вниз</p>
      <p class="text"><span class="text-button">SHIFT</span> + <span class="text-button">TAB</span> перемещаться по списку вверх</p>
    </div>
    </div>
  </div>
</template>

<script>
import Tree from "./components/Tree.vue";
import collections from "../public/static/node_modules.json";
export default {
  data: () => ({
    tree: collections,
    path: '',
    last: null
    
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



  focus: function (event) {
if(event.code == 'Enter' && event.target.parentElement.classList.contains('folder')) {
    event.target.parentElement.lastElementChild.classList.toggle('toggle')
  }
  this.createPath(event)
  }
  },
  mounted() {
    document.addEventListener('keydown',this.focus) 
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
*:focus {
outline: 3px double #596e3d;
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

.navigations {
  font-size: 20px;
  margin-bottom: 10px;
}

.text:not(:last-child) {
  margin-bottom: 15px;
}

.path {
  font-size: 15px;
}

.info {
  padding: 1rem;
  display: flex;
  border-radius: 10px;
  box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.2);
  background: #fff;
  align-items: center;
}

.info:not(:last-child) {
margin-bottom: 20px;
}

.info:last-child {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.text-button {
  border: 3px solid #6b6767;
    padding: 1px;
    background: black;
    color: white;
}
.card {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  max-height: 101px;
}

.toggle {
display: none;
}
</style>
