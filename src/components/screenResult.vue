<template>
  <div class="result">
     <span class="t">筛选条件：</span>
     <div class="c">
       <span class="item item1" v-if="fixed">跟进时间：0-7天</span>
       <span v-for="item in resultData" :key="item.id" class="item">
          {{item.name}}：<span v-for="tag in item.list" :key="tag.id">{{tag.name}}<Icon type="ios-close" @click="delOption(item.id,tag.id)"/></span>
       </span>
     </div>
     <Button type="text" @click="clear">全部清除</Button>
  </div>
</template>

<script>
export default {
  props: ["fixed"],
  data () {
    return {
      resultData:[]
    }
  },
  created() {
    $eventHub.$on("add-filter",this.addFilter);
  },
  mounted(){
    
  },
  methods:{
    addFilter(val){   
      let index = this.resultData.findIndex(opt => {
        return opt.id == val.id
      })
      if(index !=-1){   //存在，移除后再添加
        this.resultData.splice(index, 1,val)
        // this.resultData.push(val)
      }else{ // 不存在，直接添加       
        this.resultData.push(val)
      }     
      // console.log(this.resultData,"接收screen组件传过来的参数")
      this.$emit("select-data",this.resultData)
    },
    //删除tag
    delOption(itemId,listId){
      let index = this.resultData.findIndex(opt => {
        return opt.id == itemId
      })
      if(index !=-1){
        this.resultData.splice(index, 1)
      }else{      
        console.log("删除的id不存在")
      }  
      $eventHub.$emit("delete-filter",listId) 
    },
    clear(){
      this.resultData = []
      this.$emit("select-data",this.resultData)
      $eventHub.$emit("delete-filter") 
    }
  },
  //销毁
  beforeDestroy(){
    $eventHub.$off("add-filter",this.addFilter);
  }  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.result{
  font-size: 14px;
  display: flex;
  margin-bottom: 20px;
  font-weight: bold;
}
.t{
  width: 100px;
  color: #333;
  font-weight: bold;
}
.c{
  flex: 1;
  text-align: left;
}
.c span.item{
  background: #cfe5f6;
  display: inline-block;
  padding: 0px 5px 0px 10px;
  color:#2290e8;
  margin-right: 10px;
}
.c span.item1{
  padding:5px 10px;
}
.c span .ivu-icon{
  font-size: 28px;
  cursor: pointer;
}
.result .ivu-btn-text{
  color: #2290e8;
}
</style>
