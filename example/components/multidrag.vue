<template>
  <div class="row">
    <div class="col-3">
      <h3>Draggable 1</h3>
      <draggable
        class="list-group"
        v-model="list1"
        :group="{
          name: 'available-components',
          pull: 'clone',
          put: false
        }"
        multi-drag
        selected-class="selected"
        @change="log"
        @select="log"
        @start="log"
        @end="log"
        @deselect="log"
        :move="log"
      >
        <div
          class="list-group-item"
          v-for="(element, index) in list1"
          :key="element.id"
        >
          {{ element.name }} {{ index }}
        </div>
      </draggable>
    </div>

    <div class="col-3">
      <h3>Draggable 2</h3>
      <draggable
        class="list-group"
        v-model="list2"
        :group="{
          name: 'selected-components',
          put: ['available-components']
        }"
        multi-drag
        selected-class="selected"
        @change="log"
        @select="log"
        :move="log"
        @deselect="log"
      >
        <div
          class="list-group-item"
          v-for="(element, index) in list2"
          :key="element.id"
        >
          {{ element.name }} {{ index }}
        </div>
      </draggable>
    </div>

    <rawDisplayer class="col-3" :value="list1" title="List 1" />

    <rawDisplayer class="col-3" :value="list2" title="List 2" />
  </div>
</template>

<style scoped>
.selected {
  color: red !important;
  background-color: rgba(255, 0, 0, 0.2) !important;
}
</style>

<script>
import draggable from "@/vuedraggable";
export default {
  name: "multi-drag",
  display: "Multi Drag",
  order: 18,
  components: {
    draggable
  },
  data() {
    return {
      list1: [
        { name: "John", id: 1 },
        { name: "Joao", id: 2 },
        { name: "Jean", id: 3 },
        { name: "Gerard", id: 4 }
      ],
      list2: [
        { name: "Juan", id: 5 },
        { name: "Edgard", id: 6 },
        { name: "Johnson", id: 7 }
      ]
    };
  },
  methods: {
    add: function() {
      this.list.push({ name: "Juan" });
    },
    replace: function() {
      this.list = [{ name: "Edgard" }];
    },
    clone: function(el) {
      return {
        name: el.name + " cloned"
      };
    },
    log: function(evt) {
      //window.console.log(evt);
    }
  }
};
</script>
