<template>
  <div>
    <input
      type="text"
      placeholder="What need to do"
      v-model="newItem"
      @keydown.enter="addNewItem()"
      class="new-item"
    />
    <div v-for="(Item,i) in Items" :key="Item.id" class="item">
      <div @dblclick="Item.edit=true" v-if="!Item.edit">
        {{ Item.title }}
      </div>
      <div><input
      type="text"
      v-model="Item.title"
      @keydown.enter="Item.edit=false"
      @blur="Item.edit=false"
      class="new-item" v-if="Item.edit"
    /></div>
      <div class="remove-item" @click="removeItem(i)">
      &times;
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  data() {
    return {
      newItem: "",
      newItemId: 3,
      Items: [
        {
          id: 1,
          title: "learn Vuejs",
          done: true,
          edit:false,
        },
        {
          id: 2,
          title: "Develop App",
          done: false,
          edit:false,
        },
      ],
    };
  },
  methods: {
    addNewItem() {
      if (this.newItem.trim().length == 0) {
        return;
      }
      this.Items.push({
        id: this.newItemId,
        title: this.newItem,
        done: false,
        edit:false,
      });
      this.newItem = "";
      this.newItemId++;
    },
    removeItem(index){
        this.Items.splice(index,1)
    }
  },
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.new-item{
    width:100%;
    padding:10px 18px;
    font-size:18px;
    margin-bottom:16px;
}
.item{
    display:flex;
    margin-bottom:12px;
    align-items:center;
    justify-content:space-between;
}
.remove-item{
    margin-left:14px;
    cursor:pointer;
    &:hover{
        color:red;
    }
}
</style>
