<template>
    <div class="callvoice padding10">
        <!-- 头部菜单 -->
        <div class="bj_white">
            <div class="top_form">
                <div class="top_list list_search">
                    <el-input placeholder="搜索客户姓名、手机、ID" v-model="search" class="input-with-select">
                        <el-button slot="append" icon="el-icon-search"></el-button>
                    </el-input>
                </div>
                <div class="top_list">
                    <el-button type="primary" @click="addkehu">添加客户</el-button>
                </div>
                <div class="clearfix"></div>
            </div>
            <!-- 头部菜单end -->
            <!-- 表格 -->
            <div class="table">
                <el-table stripe :data="userList.slice((page_index-1)*page_size,page_index*page_size)" style="width: 100%" @row-click="openDetails">
                    <el-table-column prop="id_kehu" label="客户ID"></el-table-column>
                    <el-table-column prop="isname" label="姓名"></el-table-column>
                    <el-table-column prop="issex" label="性别"></el-table-column>
                    <el-table-column prop="birthday" label="年龄"></el-table-column>
                    <el-table-column prop="city" label="城市"></el-table-column>
                    <el-table-column prop="mobile" label="手机号"></el-table-column>
                    <el-table-column prop="beizhu" label="备注"></el-table-column>
                    <el-table-column prop="budget" label="预算" 
                    :filters="in_budget"
                    :filter-method="filterbudget"
                    filter-placement="bottom-end"></el-table-column>
                    <el-table-column prop="state" label="状态" 
                    :filters="in_state"
                    :filter-method="filterTag"
                    filter-placement="bottom-end"></el-table-column>
                </el-table>
                <!-- 分页 -->
                <page-nation :total="userList.length" @pageChange="pageChange"></page-nation>
                <!-- 分页end -->
            </div>
            <!-- 表格end -->
        </div>
    </div>
</template>
<script>
import pageNation from '@/components/pageNation/index'     // 引入分页
  export default {
    data() {
      return {
        search:'',//搜索
        page_index: 1, // 初始页
	    page_total: 200, // 总数据条数
        page_size: 8,//每页数量
        userList: [],//table数据
        in_budget:[
                { text: '1W以下', value: '1W以下' },
                { text: '1-5W', value: '1-5W' },
                { text: '6-10W', value: '6-10W' },
                { text: '10-20W', value: '10-20W' },
                { text: '20万以上', value: '20万以上' }
                ],
        in_state:[
                { text: '未处理', value: '未处理' },
                { text: '待跟进', value: '待跟进' },
                { text: '待约见', value: '待约见' },
                { text: '邀约上门', value: '邀约上门' },
                { text: '已上门-未谈妥', value: '已上门-未谈妥' },
                { text: '已上门-资质不符', value: '已上门-资质不符' },
                { text: '已交费', value: '已交费' },
                { text: '捣乱', value: '捣乱' },
                { text: '资质不符', value: '资质不符' },
                { text: '外地', value: '外地' },
                ]
      };
    },
    created: function () {
        //表格渲染
        this.handleUserList();
    },
    components: {
      pageNation
    },
    methods: {
        //添加客户
        addkehu(){
            this.$router.push({ name:'addminebox'})
        },
        //打开详情页弹窗
        openDetails(row) {
            // alert(row.id_kehu);
            this.$router.push({ name:'minedetail', query: { id: row.id_kehu }})
        },
        //表导航筛选
        //预算
        filterbudget(value, row) {
            return row.budget === value;
        },
        //状态
        filterTag(value, row) {
            return row.state === value;
        },
        // 初始页page_index、初始每页数据数page_size和数据data
        pageChange (item) {
          console.log(item)
          this.page_index = item.page_index;
          this.page_size = item.page_limit;
          // this.initData() //改变页码，重新渲染页面
        },
        handleUserList() {
            //表格渲染
            let _this = this;
            _this.axios.get('/api/wodekehu').then((res)=>{
                console.log(res.data.data);
                _this.userList = res.data.data
            }).catch((err)=>{
                console.log(err);
            })
        }
    }
  };
</script>
<style >
    .top_form .top_list{
        width: 220px;float: left;margin-right: 15px;
    }
    .top_form .list_search{
        width: 300px;
    }
    .table{
        width: 100%;margin-top: 15px;display: inline-block
    }
    .el-pagination{text-align: center;margin-top: 15px;}
</style>