<template>
    <div>
        <el-rate
  v-model="value"
  show-text>
</el-rate>
<br><br>
<el-input v-model="input" placeholder="请评论"></el-input>
<br><br>
<el-button type="primary" plain @click="back">主要按钮</el-button>
        </div>        
</template>
    


<script>
  export default {
    data() {
      return {
        value: null,
        input:'',
      }
    },
    methods:{
        back(){
            location.href='#/bookbuy'
        }
    }
  }
</script>