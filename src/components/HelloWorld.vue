<template>
  <div class="hello">
<!-- 表单A -->
      <el-card class="box-card" v-if="yourSee[0]">
      <div slot="header" class="clearfix">
        <span>表单A</span>
      </div>
         <el-form :rules="rules" :inline="true" ref="formFirst" :model="formOne" class="demo-form-inline">
            <el-form-item label="审批人"  prop="user">
            <el-input v-model="formOne.user" placeholder="审批人"></el-input>
          </el-form-item>
          <el-form-item label="活动区域" prop="region">
            <el-input v-model="formOne.region" placeholder="活动区域"></el-input>
          </el-form-item>
        </el-form>
</el-card>
<!-- 表单B -->
 <el-card class="box-card" v-if="yourSee[1]">
      <div slot="header" class="clearfix">
        <span>表单B</span>
      </div>
         <el-form :rules="rules" :inline="true" ref="formSecond" :model="formTwo" class="demo-form-inline">
            <el-form-item label="审批人"  prop="user">
            <el-input v-model="formTwo.user" placeholder="审批人"></el-input>
          </el-form-item>
          <el-form-item label="活动区域" prop="region">
            <el-input v-model="formTwo.region" placeholder="活动区域"></el-input>
          </el-form-item>
        </el-form>
</el-card>
<!-- 表单C -->
 <el-card class="box-card" v-if="yourSee[2]">
      <div slot="header" class="clearfix">
        <span>表单C</span>
      </div>
         <el-form :rules="rules" :inline="true" ref="formThird" :model="formThree" class="demo-form-inline">
            <el-form-item label="审批人"  prop="user">
            <el-input v-model="formThree.user" placeholder="审批人"></el-input>
          </el-form-item>
          <el-form-item label="活动区域" prop="region">
            <el-input v-model="formThree.region" placeholder="活动区域"></el-input>
          </el-form-item>
        </el-form>
</el-card>
<el-row type="flex" justify="center">
  <el-button type="primary" plain @click="enterForm">提交</el-button>
</el-row>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  mounted(){
    this.init()
  },
  data () {
    return {
      formOne:{user:'',region:''},
      formTwo:{user:'',region:''},
      formThree:{user:'',region:''},
      dataPick:[{user:'',region:''},{user:'',region:''},{user:'',region:''}],
      yourSee:[true,true,true],//初始权限
      xm:[true,false,false],//模拟用户小明的权限
      xh:[true,false,true],//模拟用户小红的权限
      rules: {//校验规则
          user: [{ required: true, message: '请输入用户名', trigger: 'blur' },],
          region: [{ required: true, message: '请选择区域', trigger: 'blur' },]
        },
         rulesformOne: {//校验规则
          user: [{ required: true, message: '请输入用户名', trigger: 'blur' },],
          region: [{ required: true, message: '请选择区域', trigger: 'blur' },]
        },
        rulesformTwo: {//校验规则
          user: [{ required: true, message: '请输入用户名', trigger: 'blur' },],
          region: [{ required: true, message: '请选择区域', trigger: 'blur' },]
        },
        rulesformThree: {//校验规则
          user: [{ required: true, message: '请输入用户名', trigger: 'blur' },],
          region: [{ required: true, message: '请选择区域', trigger: 'blur' },]
        }
        }
  },
  methods:{
    init(){//初始化数据，模拟用户的权限，控制哪些表单会显示
    // this.yourSee=this.xm//模拟小明同学的权限
  },
  enterForm(){//表单提交
    console.log(this.$refs['formFirst'])
   this.$refs['formFirst','formSecond','formThird'].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
  }
  }
}
</script>

<style scoped>
.box-card{
  margin-bottom:30px;
}
</style>
