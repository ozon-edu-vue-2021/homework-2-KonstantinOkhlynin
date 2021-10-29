<template>
  <li class="node-tree"  :class="activeClass(node.type, node.name)"  >
    <span @click="isActive = !isActive" v-if="node.type === 'directory' || node.type === 'file'" tabindex="0"  class="name">{{
      node.name
    }}</span>

    <a @click="isActive = !isActive" v-else tabindex="0"  :href="node.target" class="name">{{
      node.name
    }}</a>

    <ul class="ul" v-if="node.contents && node.contents.length" :class="{toggle: isActive}" >
      <node
        v-for="(child, idx) in node.contents"
        :node="child"
        :key="idx"
      ></node>
    </ul>
  </li>
</template>

<script>



export default {
  name: "node",
  props: {
    node: Object,
  },
  data() {
    return {
      isActive: true,
      mdRegex: /\.m?md$/,
      jsRegex: /\.m?js$/,
      jsonRegex: /\.m?json$/,
    };
  },
  methods: {
    activeClass: function(t, n) {
      let type = t;
      let name = n;
      if (type === "file") {
        if (this.mdRegex.test(name)) {
          return { "file-md": true };
        } else if (this.jsRegex.test(name)) {
          return { "file-js": true };
        } else if (this.jsonRegex.test(name)) {
          return { "file-json": true };
        } else {
          return { file: true };
        }
      } else if (type === "directory") {
        return { folder: true };
      } else if (type === "link") {
        return { link: true };
      }
    },

  },

  
};
</script>
<style>
.file-js {
  position: relative;
}

.file-js::before {
  content: "";
  top: 0;
  left: 2px;
  width: 20px;
  height: 20px;
  position: absolute;
  background-image: url("../assets/js.svg");
}

.file-json {
  position: relative;
}

.file-json::before {
  content: "";
  top: 0;
  left: 2px;
  width: 20px;
  height: 20px;
  position: absolute;
  background-image: url("../assets/json.svg");
}

.file-md {
  position: relative;
}

.name {
  cursor: pointer;
}

.file-md::before {
  content: "";
  top: 0;
  left: 2px;
  width: 20px;
  height: 20px;
  position: absolute;
  background-image: url("../assets/md.svg");
}

.file {
  position: relative;
}

.file::before {
  content: "";
  top: 0;
  left: 2px;
  width: 20px;
  height: 20px;
  position: absolute;
  background-image: url("../assets/file.svg");
}

li .folder {
  border-left: 1px solid #d3d3d3;
  padding-left: 25px;
}
.folder {
  position: relative;
}

.folder::before {
  content: "";
  top: 0;
  left: 2px;
  width: 20px;
  height: 20px;
  position: absolute;
  background-image: url("../assets/folder.svg");
}

.link {
  position: relative;
}

.link::before {
  content: "";
  top: 0;
  left: 2px;
  width: 20px;
  height: 20px;
  position: absolute;
  background-image: url("../assets/link.svg");
}

.toggle {
display: none;
}
</style>