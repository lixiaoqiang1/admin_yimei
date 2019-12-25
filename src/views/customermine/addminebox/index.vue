<template>
    <div class="callvoice padding10">
        <el-row :gutter="20">
            <!-- 左边 客户跟进 -->
            <el-col :span="10">
                <div class="grid-content bg-purple content_right">
                    <h4 class="title">客户基本资料 <el-button type="primary" size="medium" round >保存</el-button></h4>
                    <el-form ref="form" :model="basic" label-width="80px">
                    <el-form-item label="* 客户姓名">
                        <el-input v-model="basic.kehu_name"></el-input>
                    </el-form-item>
                    <el-form-item label="* 手机号">
                        <el-input v-model="basic.mobile"></el-input>
                    </el-form-item>
                    <el-form-item label="性别">
                        <el-radio v-model="basic.sex" label="男">男</el-radio>
                        <el-radio v-model="basic.sex" label="女">女</el-radio>
                    </el-form-item>
                    <el-form-item label="城市">
                        <v-distpicker hide-area  :province="basic.province" :city="basic.city"></v-distpicker>
                    </el-form-item>
                    <el-form-item label="出生日期">
                        <el-date-picker
                        v-model="basic.data1"
                        type="date"
                        placeholder="选择日期">
                        </el-date-picker>
                    </el-form-item>
                    </el-form>
                </div>
            </el-col>
            <!-- 右边 客户基本资料end -->
        </el-row>
    </div>
</template>
<script>
import VDistpicker from 'v-distpicker'
  export default {
    data() {
      return {
        basic: {
            kehu_name:'请输入',
            mobile:'请输入',
            sex:'男',
            selectdata1:'请输入',//日期选择
            province: '广东省',
            city: '广州市'
            
        },
      }
    },
    components: { VDistpicker },
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