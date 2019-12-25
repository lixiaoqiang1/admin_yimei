<template>
    <div class="callvoice">
        <el-row :gutter="20">
            <!-- 左边 客户跟进 -->
            <el-col :span="16" style="padding-right:0">
                <div class="grid-content bg-purple">
                    <h4>客户跟进</h4>
                    <el-form :inline="true" :model="formInline" class="demo-form-inline formInline">
                        <el-form-item label="客户预算">
                            <el-select  v-model="formInline.yusuan" placeholder="请选择">
                                <el-option
                                v-for="item in formInline.v_yusuan"
                                :key="item.yusuan"
                                :label="item.label"
                                :value="item.yusuan">
                                </el-option>
                            </el-select>
                        </el-form-item>
                        <el-form-item label="处理状态">
                            <el-select  v-model="formInline.state" placeholder="请选择">
                                <el-option
                                v-for="item in formInline.v_state"
                                :key="item.state"
                                :label="item.label"
                                :value="item.state">
                                </el-option>
                            </el-select>
                        </el-form-item>
                        <div class="beizhu">
                            <h5>跟进备注</h5>
                            <div class="inputin">
                                <el-input type="textarea"  v-model="formInline.chuli_text" :rows="2" placeholder="请输入内容"></el-input>
                                <el-button type="primary">确定</el-button>
                            </div>
                        </div>
                        
                    </el-form>
                    <h5>跟进历史</h5>
                    <el-timeline>
                        <el-timeline-item  placement="top"
                        v-for="(activity, index) in activities"
                        :key="index"
                        :timestamp="activity.timestamp">
                        {{activity.content}}
                        </el-timeline-item>
                    </el-timeline>
                </div>
            </el-col>
            <!-- 左边 客户跟进end -->
            <!-- 右边 客户基本资料 -->
            <el-col :span="8">
                <div class="grid-content bg-purple content_right">
                    <h4 class="title">客户基本资料 <el-button type="primary"  round >保存</el-button></h4>
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
                <div class="grid-content bg-purple content_down">
                    <div class="listbtn">
                        <el-button  type="primary" plain round>转给其他顾问</el-button><span>需转给其他顾问跟进的客户</span>
                    </div>
                    <div class="listbtn">
                        <el-button  type="danger" plain round>丢进公共池</el-button><span>自己跟不下来的客户，可丢进公共池</span>
                    </div>
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
        formInline: {
            yusuan:'',
            v_yusuan:[
                {value: '1万以下',label: '1万以下'},
                {value: '1-5万',label: '1-5万'},
                {value: '6-10万',label: '6-10万'},
                {value: '11-20万',label: '11-20万'}
            ],
            state:'',
            v_state:[
                {value: '未处理',label: '未处理'},
                {value: '待跟进',label: '待跟进'},
                {value: '待约见',label: '待约见'},
                {value: '邀约上门',label: '邀约上门'},
                {value: '已上门-未谈妥',label: '已上门-未谈妥'},
                {value: '已上门-资质不符',label: '已上门-资质不符'},
                {value: '已交费',label: '已交费'},
                {value: '捣乱',label: '捣乱'},
                {value: '资质不符',label: '资质不符'},
                {value: '外地',label: '外地'}
            ],
            chuli_text:'请输入',
        },
        activities: [
            {content: '陈锋：待约见',timestamp: '2018-04-15' },
            {content: '陈锋：待约见',timestamp: '2018-04-15' },
            {content: '陈锋：待约见',timestamp: '2018-04-15' }
            ],
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
  .callvoice .el-col-16{
      padding-right: 0
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
  .inputin{
      position: relative;
  }
 .inputin .el-textarea__inner {
    min-height: 33px;resize: none;height: 80px;padding-right: 70px;
  }
  .inputin button{
      position: absolute;right: 0;top: 0; height: 80px;
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
  .content_down{
      margin-top: 10px;font-size: 14px;color: #666
  }
  .content_down .listbtn{
      margin: 15px 0;
  }
  .content_down .listbtn button{
      min-width: 150px;margin-right: 10px
  }
</style>