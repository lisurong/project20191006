<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <!--筛选结果,有近期7天的固定字段，配置:fixed="true"-->
    <result @select-data="selectLsitFun"></result>  
    <!--筛选数据-->
    <screen :screen="item" v-for="item in calcLength(screenList)" :key="item.id"></screen> 
   <!--展开收起,默认多余三项显示展开收起。如果修改这里，需要改screenList.length>3和data里面的limitLength的数量-->
    <div class="fold" v-if="screenList.length>3">
      <span @click="onPickUp">{{pickUpMsg}}</span>
      <Icon @click="onPickUp" color="#2290E8;" type="ios-arrow-up" />
    </div>
  </div>
</template>

<script>
import result from './screenResult.vue'
import screen from './screen.vue'
export default {
  components:{
    screen,
    result
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      pickUpMsg: '展开',
      pickUp: true,     // 显示收起/展开
      limitLength:3,
      screenList:[
        {
          id:1,
          name:"跟进时间",
          list:[
            {
              id:101,
              name:"0-7天"
            },
            {
              id:102,
              name:"8-15天"
              
            },
            {
              id:103,
              name:"自定义"
              
            }
          ]
        },{
          id:2,
          name:"跟进人",
          list:[
            {
              id:201,
              name:"张三"
            },{
              id:202,
              name:"李四"
              
            },{
              id:204,
              name:"赵武"
              
            },
            {
              id:205,
              name:"赵武"
              
            },
            {
              id:206,
              name:"赵武"
              
            },
            {
              id:207,
              name:"赵武"
              
            },
            {
              id:208,
              name:"赵武"
              
            },
            {
              id:209,
              name:"赵武"
              
            },
            {
              id:210,
              name:"赵武"
              
            },
            {
              id:211,
              name:"赵武"
              
            },
            {
              id:212,
              name:"赵武"
              
            },
            {
              id:213,
              name:"赵武"
              
            },
            {
              id:214,
              name:"李素荣"
              
            }
          ]
        },
       {
          id:3,
          name:"跟进方式",
          list:[
            {
              id:301,
              name:"微信"
            },
            {
              id:302,
              name:"QQ"
              
            },
            {
              id:303,
              name:"拜访"
              
            }
          ]
        }
      ]
    }
  },
  methods:{
    calcLength(list){
      if (list.length > this.limitLength && this.pickUp) {
        return list.slice(0, this.limitLength);
      } else {
        return list;
      }
    },
    onPickUp(){
      if(this.pickUp) {
        this.pickUp = false
        this.pickUpMsg = '收起'
      }else {
        this.pickUp = true
        this.pickUpMsg = '展开'
      }
    },
    //父组件接收选择的数据
    selectLsitFun(val){
      console.log(val,"父组件接收选择的数据")
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.fold span{
  font-size: 16px;
}
.screen-r{
  background-color: #fbfbfb;
  border: 1px solid #ddd;
}
.screen-s{
  background-color: #fbfbfb;
  border: 1px solid #ddd;
  border-top:none;
}
</style>
