<template>
    <div class="callvoice padding10">
        <el-row :gutter="20">
            <!-- 左边 客户跟进 -->
            <el-col :span="10">
                <div class="grid-content bg-purple content_right">
                    <h4 class="title">团队成员 <el-button type="primary" size="medium" round >保存</el-button></h4>
                    <el-form ref="form" :model="basic" label-width="80px">
                        <el-form-item label="客户姓名">
                            <el-input v-model="basic.kehu_name"></el-input>
                        </el-form-item>
                        <el-form-item label="手机号">
                            <el-input v-model="basic.mobile"></el-input>
                        </el-form-item>
                        <el-form-item label="计划日分配数">
                            <el-input v-model="basic.fenpei"></el-input>
                        </el-form-item>
                        <el-form-item label="新数据开关">
                            <el-radio v-model="basic.shuju" label="开启">开启</el-radio>
                            <el-radio v-model="basic.shuju" label="关闭">关闭</el-radio>
                        </el-form-item>
                        <el-form-item label="是否允许登录">
                            <el-radio v-model="basic.shuju" label="允许登录">允许登录</el-radio>
                            <el-radio v-model="basic.yunxu" label="禁止登录">禁止登录</el-radio>
                        </el-form-item>
                    </el-form>
                </div>
            </el-col>
            <!-- 右边 客户基本资料end -->
        </el-row>
    </div>
</template>
<script>
  export default {
    data() {
      return {
        basic: {
            kehu_name:'请输入',
            mobile:'请输入',
            fenpei:'10',
            shuju:'开启',
            yunxu:'允许登录'
            
            
        }
      }
    }
   
  };
</script>
<style>
  .bg-purple {
    background: #ffffff;padding: 20px;
  }
  .callvoice h5{
      margin: 0;padding: 0;line-height: 36px
  }
  .callvoice h4{
      margin: 0;padding: 0;line-height: 50px
  }
  .el-form-item{
      margin-bottom: 15px
  }
  .el-timeline{
      padding: 20px 0 0 10px;
  }
  .distpicker-address-wrapper select{
      width: 49%;
  }
  .el-date-editor.el-input{
      width: 100%;
  }
  .content_right .title button{
      float: right
  }

</style>