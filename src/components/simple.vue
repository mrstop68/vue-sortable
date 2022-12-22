<template>
    <div class="row">
      <div class="col-6 opacitySort">
        <h3>Draggable</h3>
  
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
  
    </div>
   <div>
    <ul id="myTable">
      <li>deneme 1 </li>
      <li>deneme 2 </li>
      <li>deneme 3 </li>
    </ul>
   </div>
  </template>
  
  <script>
  import draggable from "vuedraggable";
  import Sortable from "sortablejs";
  let id = 1;
  export default {
    name: "simpleS",
    display: "Simple",
    order: 0,
    components: {
      draggable,
    },
    data() {
      return {
        options: {
                handle: '.handle',
                filter: '.disabled'
            },
        enabled: true,
        myArray: [
          { name: "Item", id: 0 },
          { name: "Item", id: 1 },
          { name: "Item", id: 2 }
        ],
        dragging: false,
        oldIndex:'',
        newIndex:'',
        sortable:''

      };
    },
    mounted() {
   const element = document.querySelector("#myTable"); // grab the element containing the <tr> elements
   this.sortable = Sortable.create(element, {
      onEnd(event) { // gets called when dragging ended
          console.log(event.oldIndex)
          console.log(event.newIndex)
      }
   });
      },
    computed: {
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