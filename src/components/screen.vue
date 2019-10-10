<template>
  <div class="screen">
      <span class="scr-l">{{screen.name}}:</span>
      <div class="scr-r">
        <span v-for="item in screen.list" :key="item.id" @click="choose(item,screen)" :class="{active:selectId && selectId==item.id}">{{item.name}}</span>
      </div>
  </div>
</template>

<script>
export default {
  props: {
    screen: {
      type: Object,
    }
  },
  data () {
    return {
      selectId:'',
      selectData:[],
    }
  },
  mounted(){
    $eventHub.$on("delete-filter",this.deleteFilter);
  },
  methods:{
    choose(item,screen){
      this.selectId = item.id
     
      let obj = {
        id:screen.id,
        name:screen.name,
        list:[item]
      }
      // this.selectData =[]
      // this.selectData.push(obj)

      $eventHub.$emit("add-filter",obj)
    },
    deleteFilter(val){
      if(val == this.selectId){
        this.selectId = null
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.screen{
  display: flex;
  height: 40px;
  font-size:16px;
}
.scr-l{
    width: 100px;
    color: #333;
    font-weight: bold;
  }
  .scr-r{
    flex: 1;
    text-align: left;

  }
  .scr-r span{
    display: inline-block;
    margin-right: 25px;
    cursor: pointer;
  }
.scr-r span.active{
  color:#ff2c0a;
}
</style>
