<template>
  <div style="display: flex;background-color: rgb(247,247,247);overflow-x: hidden;">
  <!-- 左侧菜单 -->
    <el-menu default-active="1-4-1" class="el-menu-vertical-demo" :collapse="isCollapse">
      <el-submenu index="1">
        <template slot="title">
          <span slot="title">沪深股市</span>
        </template>
        <el-menu-item-group>
          <el-menu-item index="1-1">趋势</el-menu-item>
          <el-menu-item index="1-2">行业</el-menu-item>
          <el-menu-item index="1-3">资讯</el-menu-item>
          <el-menu-item index="1-4">对比</el-menu-item>
        </el-menu-item-group>
      </el-submenu>
      <el-submenu index="2">
        <template slot="title">
          <span slot="title">北交所</span>
        </template>
        <el-menu-item-group>
          <el-menu-item index="2-1">趋势</el-menu-item>
          <el-menu-item index="2-2">资讯</el-menu-item>
        </el-menu-item-group>
      </el-submenu>
      <el-submenu index="3">
        <template slot="title">
          <span slot="title">自选股票</span>
        </template>
        <el-menu-item-group>
          <el-menu-item index="3-1">沪深</el-menu-item>
          <el-menu-item index="3-2">北交所</el-menu-item>
        </el-menu-item-group>
      </el-submenu>
      <el-submenu index="4">
        <template slot="title">
          <span slot="title">其他参考</span>
        </template>
        <el-menu-item-group>
          <el-menu-item index="4-1">上市公司行情指数</el-menu-item>
        </el-menu-item-group>
      </el-submenu>
    </el-menu>
<!-- 右侧数据 -->
    <div style="flex:1;">
      <el-input placeholder="请输入内容"></el-input>
      <div class="box-list">
        <div class="box-list-two" v-for="item,i in boxListData" :key="i">
          <h3>{{item.name}}</h3>
          <p>{{item.price}}</p>
          <p>{{item.change}}</p>
        </div>
      </div>
      <el-row :gutter="20">
        <el-col :span="10"><div class="box-list-box" id="threeLeft"></div></el-col>
        <el-col :span="14"><div class="box-list-box" id="threeRight"></div></el-col>
      </el-row>
      <el-row :gutter="20">
        <el-col :span="14"><div id="threeLeft1" class="box-list-box"></div></el-col>
        <el-col :span="10"><div class="box-list-box">
          <h3 style="margin: 10px;">行业涨跌排名</h3>
          <el-table
            :data="tableData.slice((currentPage-1)*pageSize,currentPage*pageSize)"
            border>
            <el-table-column
              prop="date"
              label="行业名称"
              width="180">
            </el-table-column>
            <el-table-column
              prop="name"
              label="涨跌幅"
              width="180">
            </el-table-column>
            <el-table-column
              prop="address"
              label="股份">
            </el-table-column>
          </el-table>
          <el-pagination
            style="position: absolute;bottom: 10%;right: 16%;"
            background
            layout="prev, pager, next"
            :page-size="pageSize"
            :current-page.sync="currentPage"
            :total="tableData.length">
          </el-pagination>
        </div></el-col>
      </el-row>
      <el-row :gutter="20">
        <el-col :span="12"><div class="box-list-box" id="threeLeft2"></div></el-col>
        <el-col :span="12"><div class="box-list-box">
          <h3 style="margin: 10px;">个股涨跌榜</h3>
          <el-table
            :data="tableData1.slice((currentPage1-1)*pageSize1,currentPage1*pageSize1)"
            border>
            <el-table-column
              prop="name"
              label="公司名称"
              width="180">
            </el-table-column>
            <el-table-column
              prop="code"
              label="公司代码"
              width="180">
            </el-table-column>
            <el-table-column
              prop="price"
              label="当前价格">
            </el-table-column>
            <el-table-column
              prop="updown"
              label="价格涨跌">
            </el-table-column>
            <el-table-column
              prop="change"
              label="涨跌幅">
            </el-table-column>
          </el-table>
          <el-pagination
            style="position: absolute;bottom: 10%;right: 20%;"
            background
            layout="prev, pager, next"
            :page-size="pageSize1"
            :current-page.sync="currentPage1"
            :total="tableData1.length">
          </el-pagination>
        </div></el-col>
      </el-row>
    </div>
    
  </div>
</template>

<script>
import * as echarts from 'echarts';
export default {
  name: 'HelloWorld',
  data() {
      return {
        isCollapse: false,
        currentPage:1,
        currentPage1:1,
        pageSize:5,
        pageSize1:6,
        boxListData:[
          {
            name: '上证指数',
            price: '31122.35',
            change: '-35.72(-1.13%)'
          },
          {
            name: '沪深300',
            price: '31122.35',
            change: '-35.72(-1.13%)'
          },
          {
            name: '中证500',
            price: '31122.35',
            change: '-35.72(-1.13%)'
          },
          {
            name: 'CR基石',
            price: '31122.35',
            change: '-35.72(-1.13%)'
          },
          {
            name: 'CR新动能',
            price: '31122.35',
            change: '-35.72(-1.13%)'
          },
          {
            name: '创业模板',
            price: '31122.35',
            change: '-35.72(-1.13%)'
          },
          {
            name: '中证1000',
            price: '31122.35',
            change: '-35.72(-1.13%)'
          },
        ],
        tableData: [{
          date: '石油石化',
          name: '+0.65%',
          address: '上海市普陀区'
        }, {
          date: '煤炭',
          name: '+0.18%',
          address: '上海市普陀区'
        }, {
          date: '社会服务',
          name: '-0.03%',
          address: '上海市普陀区'
        }, {
          date: '银行',
          name: '-0.14%',
          address: '上海市普陀区'
        }, {
          date: '通信',
          name: '-0.56%',
          address: '上海市普陀区'
        }, {
          date: '纺织服饰',
          name: '-0.71%',
          address: '上海市普陀区'
        }, {
          date: '金融',
          name: '-0.72%',
          address: '上海市普陀区'
        }],
        tableData1: [{
          name: '星星科技',
          code:"11111",
          price:"3.71",
          updown:"+0.62%",
          change:"+20.60%",
        }, {
          name: '职美信息',
          code:"22222",
          price:"15.71",
          updown:"+2.62%",
          change:"+20.02%",
        }, {
          name: '佼佼股份',
          code:"33333",
          price:"56.64",
          updown:"+9.44%",
          change:"+20.00%",
        }, {
          name: '华立科技',
          code:"44444",
          price:"24.67",
          updown:"+4.11%",
          change:"+19.99%",
        }, {
          name: '电声股份',
          code:"55555",
          price:"9.71",
          updown:"+1.25%",
          change:"+14.76%",
        }, {
          name: '华信科技',
          code:"66666",
          price:"13.34",
          updown:"+1.68%",
          change:"+14.41%",
        }, {
          name: '王小虎',
          code:"11111",
          price:"3.71",
          updown:"+0.00%",
          change:"+0.00%",
        }, {
          name: '王小虎',
          code:"11111",
          price:"3.71",
          updown:"+0.00%",
          change:"+0.00%",
        }, {
          name: '王小虎',
          code:"11111",
          price:"3.71",
          updown:"+0.00%",
          change:"+0.00%",
        }, {
          name: '王小虎',
          code:"11111",
          price:"3.71",
          updown:"+0.00%",
          change:"+0.00%",
        }, {
          name: '王小虎',
          code:"11111",
          price:"3.71",
          updown:"+0.00%",
          change:"+0.00%",
        }, {
          name: '王小虎',
          code:"11111",
          price:"3.71",
          updown:"+0.00%",
          change:"+0.00%",
        }, {
          name: '王小虎',
          code:"11111",
          price:"3.71",
          updown:"+0.00%",
          change:"+0.00%",
        }, {
          name: '王小虎',
          code:"11111",
          price:"3.71",
          updown:"+0.00%",
          change:"+0.00%",
        }, {
          name: '王小虎',
          code:"11111",
          price:"3.71",
          updown:"+0.00%",
          change:"+0.00%",
        }]
      };
    },
    created(){

    },
    mounted() {
      this.threeLeft();
      this.threeRight();
      this.threeLeft1();
      this.threeLeft2();
    },
    methods: {
      threeLeft(){
        var chartDom = document.getElementById('threeLeft');
        var myChart = echarts.init(chartDom);
        var option;
        
        let base = +new Date(1988, 9, 3);
        let oneDay = 24 * 3600 * 1000;
        let data = [[base, Math.random() * 300]];
        for (let i = 1; i < 20000; i++) {
          let now = new Date((base += oneDay));
          data.push([+now, Math.round((Math.random() - 0.5) * 20 + data[i - 1][1])]);
        }
        
        option = {
          tooltip: {
            trigger: 'axis',
            position: function (pt) {
              return [pt[0], '10%'];
            }
          },
          title: {
            left: 'left',
            text: '上证指数'
          },
          toolbox: {
            feature: {
              dataZoom: {
                yAxisIndex: 'none'
              },
              restore: {},
              saveAsImage: {}
            }
          },
          xAxis: {
            type: 'time',
            boundaryGap: false
          },
          yAxis: {
            type: 'value',
            boundaryGap: [0, '100%']
          },
          dataZoom: [
            {
              type: 'inside',
              start: 0,
              end: 20
            },
            {
              start: 0,
              end: 20
            }
          ],
          series: [
            {
              name: 'Fake Data',
              type: 'line',
              smooth: true,
              symbol: 'none',
              areaStyle: {},
              data: data
            }
          ]
        };
        option && myChart.setOption(option);
      },
      threeRight(){
        var chartDom = document.getElementById('threeRight');
        var myChart = echarts.init(chartDom);
        var option;

        option = {
          series: [
            {
              type: 'treemap',
              data: [
                {
                  name: 'nodeA',
                  value: 10,
                  children: [
                    {
                      name: 'nodeAa',
                      value: 4
                    },
                    {
                      name: 'nodeAb',
                      value: 6
                    }
                  ]
                },
                {
                  name: 'nodeB',
                  value: 20,
                  children: [
                    {
                      name: 'nodeBa',
                      value: 20,
                      children: [
                        {
                          name: 'nodeBa1',
                          value: 20
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ]
        };

        option && myChart.setOption(option);
      },
      threeLeft1(){
        var chartDom = document.getElementById('threeLeft1');
        var myChart = echarts.init(chartDom);
        var option;

        option = {
          xAxis: {
            type: 'category',
            data: ['行业1', '行业2', '行业3', '行业4', '行业5', '行业6', '行业7', '行业8', '行业9', '行业10', '行业11', '行业12', '行业13', '行业14', '行业15', '行业16']
          },
          yAxis: {
            type: 'value'
          },
          title: {
            left: 'left',
            text: '个股涨跌情况'
          },
          series: [
            {
              data: [
              {
                  value: 1,
                  itemStyle: {
                    color: 'red'
                  }
                },{
                  value: 2,
                  itemStyle: {
                    color: 'red'
                  }
                },
                -0.1,
                -0.2,
                -0.3,
                -0.4,
                -0.5,
                -0.6,
                -0.7,
                -0.8,
                -0.9,
                -1,
                -1.1,
                -1.2,
                -2,
                -4,
              ],
              type: 'bar'
            }
          ]
        };

        option && myChart.setOption(option);
      },
      threeLeft2(){
        var chartDom = document.getElementById('threeLeft2');
        var myChart = echarts.init(chartDom);
        var option;

        option = {
          xAxis: {
            type: 'category',
            data: ['上涨', '平盘', '下跌', '停止']
          },
          yAxis: {
            type: 'value'
          },
          title: {
            left: 'left',
            text: '个股涨跌情况'
          },
          series: [
            {
              data: [
              {
                  value: 457,
                  itemStyle: {
                    color: 'red'
                  }
                },
                57,
                {
                  value: 4537,
                  itemStyle: {
                    color: 'lightgreen'
                  }
                },
                2,
              ],
              type: 'bar'
            }
          ]
        };

        option && myChart.setOption(option);
      }
    }
}
</script>

<style scoped>
*{
  margin: 0;
  padding: 0;
}
/* 在浏览器宽度小于1200px时隐藏侧方导航栏菜单 */
@media (max-width: 1200px) {
    .el-menu-vertical-demo {
        display: none;
    }
}
.el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 200px;
    height: 100%;
    margin-right: 10px;
  }
.box-list{
  display: flex;
  justify-content: space-around;
  margin: 10px;
}
.box-list .box-list-two{
  width: 200px;
  height: 100px;
  background-color: rgb(219,254,235);
  margin: 5px;
  border-radius: 5px;
}
:where(.box-list .box-list-two) h3,p {
  margin: 7px;
}
.box-list .box-list-two h3{
  color:rgb(141,135,238);
}
.box-list .box-list-two p{
  color:rgb(128,225,172);
}
.box-list-box{
  min-height: 500px;
  background-color: #fff;
  margin: 10px;
  padding: 10px;
  border-radius: 5px;
}
</style>
