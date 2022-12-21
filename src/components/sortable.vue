<template>
    <div class="row">
      <div class="col-2">
        <div class="form-group">
          <div
            class="btn-group-vertical buttons"
            role="group"
            aria-label="Basic example"
          >
            <button class="btn btn-secondary" @click="add">Add</button>
            <button class="btn btn-secondary" @click="replace">Replace</button>
          </div>
  
          <div class="form-check">
            <input
              id="disabled"
              type="checkbox"
              v-model="enabled"
              class="form-check-input"
            />
            <label class="form-check-label" for="disabled">DnD enabled</label>
          </div>
        </div>
      </div>
  
      <div class="col-6 opacitySort">
        <h3>Draggable {{ draggingInfo }}</h3>
  
        <draggable
          :list="myArray"
          :disabled="!enabled"
          item-key="name"
          class="list-group"
          ghost-class="ghost"
          :move="checkMove"
          @start="dragging = true"
          @end="dragging = false"
          
        >
       
        <template #item="{ element }">
            <div class="list-group-item" :class="{ 'not-draggable': !enabled }" name="flip-list">
              {{ element.name }}
              <span>{{element.id }}</span>
            </div>
        </template>
        
         
        </draggable>
        <div><ul><li>Old Index: {{ oldIndex }}</li></ul></div>
        <div><ul><li>New Index: {{ newIndex }}</li></ul></div>
       
      </div>
  
      <rawDisplayer class="col-3" :value="list" title="List" />
    </div>
  </template>
  
  <script>
  import draggable from "vuedraggable";
  let id = 1;
  export default {
    name: "simpleS",
    display: "Simple",
    order: 0,
    components: {
      draggable
    },
    data() {
      return {
        enabled: true,
        myArray: [
          { name: "John", id: 0 },
          { name: "Joao", id: 1 },
          { name: "Jean", id: 2 }
        ],
        dragging: false,
        oldIndex:'',
        newIndex:''
      };
    },
    computed: {
      draggingInfo() {
        return this.dragging ? "under drag" : "";
      },
      dragOptions() {
      return {
        animation: 200,
        group: "description",
        disabled: false,
        ghostClass: "ghost"
      };
    }
    },
    methods: {
      add: function() {
        this.myArray.push({ name: "Juan " + id, id: id++ });
      },
      replace: function() {
        this.myArray = [{ name: "Edgard", id: id++ }];
      },
      checkMove: function(e) {
        window.console.log("Future index: " + e.draggedContext.futureIndex);
        console.log(e.draggedContext)
        this.oldIndex=e.draggedContext.index;
        this.newIndex=e.draggedContext.futureIndex;
      }
    }
  };
  </script>
  <style scoped>
  .buttons {
    margin-top: 35px;
  }
  .ghost {
    opacity: 0.5;
    background: #c8ebfb;
  }
  .not-draggable {
    cursor: no-drop;
  }
  .list-group {
  min-height: 20px;
}
  .list-group-item{
    padding: 1em;
    border: 1px solid #c8ebfb;
    cursor: move;
    margin-bottom: 2px;
    }
    .list-group-item i {
  cursor: pointer;
}
    .opacitySort .sortable-drag{
        opacity: 0;

    }
    .flip-list-move {
        transition: transform 0.5s;
    }
    .no-move {
  transition: transform 0s;
}
.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}

  </style>