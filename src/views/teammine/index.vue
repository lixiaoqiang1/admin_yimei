<template>
    <div class="callvoice padding10">
        <!-- 头部菜单 -->
        <div class="bj_white">
            <div class="top_form">
                <div class="top_list list_search">
                    <el-input placeholder="搜索员工姓名、手机" v-model="search" class="input-with-select">
                        <el-button slot="append" icon="el-icon-search"></el-button>
                    </el-input>
                </div>
                <div>
                    <el-button type="primary" @click="addkehu">批量关数据</el-button>
                    <el-button type="primary">批量禁止登录</el-button>
                </div>
                
            </div>
            <!-- 头部菜单end -->
            <!-- 表格 -->
            <div class="table">
                <el-table stripe :data="userList.slice((page_index-1)*page_size,page_index*page_size)" style="width: 100%" @selection-change="handleSelectionChange">
                    <el-table-column type="selection" width="55" :reserve-selection="true"> </el-table-column>
                    <el-table-column prop="isname" label="顾问姓名"></el-table-column>
                    <el-table-column prop="mobile" label="顾问手机"></el-table-column>
                    <el-table-column prop="plan" label="计划日分配数"></el-table-column>
                    <el-table-column prop="actual" label="实际分配数"></el-table-column>
                    <el-table-column prop="existing" label="现有客户数"></el-table-column>
                    <el-table-column prop="new_data" label="新数据开关">
                        <template slot-scope="scope">
                            <div>
                            
                            </div>
                        </template>
                    </el-table-column>
                    <el-table-column prop="ifnot" label="是否允许登录">
                        <template slot-scope="scope">
                            <div class="fund_box"> 
                                <a class="{ischeck == index ? 'active':''}" @click="activeClick(1,scope.row)">开启</a>
                                <a class="{ischeck == index ? 'active':''}" @click="activeClick(2,scope.row)">关闭</a>
                            </div>
                        </template>
                    </el-table-column>
                    <el-table-column label="操作">
                        <template slot-scope="scope">
                            <el-button @click="editorClick(scope.$index, scope.row)" type="text" size="small">编辑</el-button>
                        </template>
                    </el-table-column>
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
        ifnotindex:'',
        current: 0,
        multipleSelection:[],//table勾选项
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
            ],
        in_belongs:[
            { text: '公共池', value: '公共池' },
            { text: '张大白', value: '张大白' },
            { text: '李大白', value: '李大白' },
        ],
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
        //打开批量分配弹层
        addkehu(row){
           console.log(row)
        },
        choice(index) {
            console.log(index)
            this.current = index;
        },
        //新数据开关
        activeClick(index,row){    
            console.log(index)           
            console.log(row.id_kehu)           
            this.ifnotindex = index;
        },
        handleSelectionChange(val) {
            this.multipleSelection = val;
        },
        //操作编辑
        editorClick(index, row){
            console.log(index, row.id_kehu);
            this.$router.push({ name:'members', query: { id: row.id_kehu }})
        },
        // 初始页page_index、初始每页数据数page_size和数据data
        pageChange (item) {
          this.page_index = item.page_index;
          this.page_size = item.page_limit;
          // this.initData() //改变页码，重新渲染页面
        },
        handleUserList() {
            //表格渲染
            let _this = this;
            _this.axios.get('/api/tuandui').then((res)=>{
                _this.userList = res.data.data
            }).catch((err)=>{
                console.log(err);
            })
        }
    }
  };
</script>
<style>
    .top_form .top_list{
        width: 220px;float: left;margin-right: 15px;
    }
    .top_form .list_search{
        width: 300px;
    }
    .table{
        width: 100%;margin-top: 15px;display: inline-block
    }
    /* .fund_box a{display: none}
    .fund_box .active{display: block} */
</style>