
<template>
<div style=" line-height: 60px; display: flex">
  <div style="flex: 1;">
    <span :class="collapseBtnClass" style="cursor: pointer; font-size: 18px" @click="collapse"></span>

    <el-breadcrumb separator="/" style="display: inline-block;margin-left: 10px">
    <el-breadcrumb-item :to="'/'">首页</el-breadcrumb-item>
      <el-breadcrumb-item>{{ currentPathName}}</el-breadcrumb-item>
  </el-breadcrumb>
  </div>
  <span>{{user.wjyType}}:{{ user.wjyName }}</span>
    <el-dropdown style=" cursor: pointer">
    <i class="el-icon-arrow-down" style="margin-left: 5px">
      <el-dropdown-menu slot="dropdown" style="width: 100px; text-align: center">
        <el-dropdown-item style="font-size: 14px; padding: 5px 0">
          <router-link to="/person" style="text-decoration: none; color: #000;">个人信息</router-link>
        </el-dropdown-item>
        <el-dropdown-item style="font-size: 14px; padding: 5px 0">
          <span style="text-decoration: none;color: #000;" @click="logout">退出</span>
        </el-dropdown-item>
      </el-dropdown-menu>
      </i>
  </el-dropdown>

</div>
</template>

<script>
import MiddleUtil from "@/utils/MiddleUtil";
export default {
  name: "Header",
  props:{
    collapseBtnClass:String,
    collapse:Function
  },
  data(){
    return{
      paths:[],
      form:{},
       user:localStorage.getItem("user")?JSON.parse(localStorage.getItem("user")):{},
    }
  },
  created() {
    MiddleUtil.$on("click",(name)=>{
      this.changeUsername(name);
    });
  },
  computed:{
    currentPathName(){
      return this.$store.state.currentPathName;　　//需要监听的数据
    }
  },

  methods:{
   logout(){
     this.$router.push("/login")
     localStorage.removeItem("user")
     this.$message.success("退出成功")//清空数据
   },
    changeUsername(name) {//动态修改昵称
      this.$set(this.user, 'name',name);
       },
  },
   mounted() {
   MiddleUtil.$on("click",(name)=>{
     this.changeUsername(name);
   });
  },
    watch: {
    currentPathName(newVal, oldVal) {
      console.log(newVal)
    }
  },

}
</script>

<style scoped>

</style>