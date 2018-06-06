<template>
  <div class="hello">
    <!-- 模拟 用户选择 -->
    <el-radio-group v-model="tabPosition" style="margin-bottom: 30px;" @change="userChange(tabPosition)">
      <el-radio-button label="xm">用户：小明</el-radio-button>
      <el-radio-button label="xh">用户：小红</el-radio-button>
    </el-radio-group>

      <el-card class="box-card" v-for="(item,index) in makeData" :key="item.index" v-if="item.formShow">
      <div slot="header" class="clearfix"><span>{{item.formName}}</span></div>
      <!-- form -->
         <el-form  :inline="true" :ref="item.formRef" :model="item.formModel" class="demo-form-inline">
            <el-form-item label="审批人" prop='user' :rules="[{ required: true, message: '审批人不能为空'}]">
               <el-input v-model="item.formModel.user" placeholder="审批人"></el-input>
            </el-form-item>
             <el-form-item label="区域" prop='region' :rules="[{ required: true, message: '区域不能为空'}]">
               <el-input v-model="item.formModel.region" placeholder="审批人"></el-input>
            </el-form-item>

        </el-form>
</el-card>
<!-- 提交 -->
<el-row type="flex" justify="center">
  <el-button type="primary" plain @click="enterForm">提交</el-button>
</el-row>
  </div>
</template>

<script>
export default {
  mounted(){
    this.userChange('xm')//模拟登录的是小明
  },
  data () {
    return {
     makeData:[{
       formRef:'formFirst',//表单ref
       formModel:{user:'',region:''},//表单model
       formShow:'',//表单是否显示的控制
       formName:'表单A'//表单标题
      },{
      formRef:'formSecond',
       formModel:{user:'',region:''},
       formShow:'',
       formName:'表单B'

      },{
        formRef:'formThird',
       formModel:{user:'',region:''},
       formShow:'',
       formName:'表单C'

      }],
      xm:[true,true,true],//用户小明的权限
      xh:[true,true,false],//用户小红的权限
      tabPosition:'xm'//选择用户
     
        }
  },
  methods:{
  
  enterForm(){//动态表单提交
    console.log(this.$refs.formFirst)

let  arrForm=[]//哪些表单需要做校验
let  arrModel=[]//表单的值
let  newArr = [] //承接promise的返回结果
let _self=this
this.makeData.forEach((item,index)=>{//将有权限的表单做校验等等
  if (item.formShow) {
      checkForm(item.formRef)//校验
      arrModel.push(item.formModel)//需要校验的表单的值
  }
})

 function checkForm(arrName) { //根据form表单的ref，动态生成promise，再对其坐表单校验，都通过了再去做处理
      var result = new Promise(function(resolve, reject) {
          _self.$refs[arrName][0].validate((valid) => {
              if (valid) {
                  resolve();
              } else { reject() }
          })
      })
      newArr.push(result) //push 得到promise的结果
}

Promise.all(newArr).then(function() { //都通过了
      console.log(arrModel)
      alert('恭喜，表单全部验证通过')
    }).catch(function() {
        console.log("err");
    });
  },
  userChange(val){//当前登录用户的change
    this.makeData.map((item,index)=>{//根据用户的权限决定显示哪些表单
      var c=item.formRef
      if (this.$refs[c]&&this.$refs[c][0]) { this.$refs[c][0].resetFields()}//模拟切换用户时，将表单置空
      return item.formShow=this[val][index]
    })
  }
  }
}
</script>

<style scoped>
.box-card{
  margin-bottom:30px;
}
</style>
