<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <result></result>
   <screen :screen="item" v-for="item in screenList" :key="item.id"></screen>
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
              
            }
          ]
        },{
          id:2,
          name:"跟进人",
          list:[
            {
              id:201,
              name:"张三"
            },
            {
              id:202,
              name:"李四"
              
            },
            {
              id:203,
              name:"赵武"
              
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
</style>
