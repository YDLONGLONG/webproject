<template>
  <div style="display: flex;">
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

    <div style="flex:1">
      <el-input placeholder="请输入内容"></el-input>
      <div class="box-list">
        <div class="box-list-two" v-for="item,i in boxListData" :key="i">
          <h3>{{item.name}}</h3>
          <p>{{item.price}}</p>
          <p>{{item.change}}</p>
        </div>
      </div>
      <div class="box-list-three">
        <div class="box-list-three-left" id="threeLeft"></div>
        <div class="box-list-three-right" id="threeRight"></div>
      </div>
      <div class="box-list-three">
        <div class="box-list-three-right" id="threeLeft1"></div>
        <div class="box-list-three-left">
          <el-table
            :data="tableData.slice((currentPage-1)*pageSize,currentPage*pageSize)"
            border
            style="width: 90%;margin: 30px;">
            <el-table-column
              prop="date"
              label="日期"
              width="180">
            </el-table-column>
            <el-table-column
              prop="name"
              label="姓名"
              width="180">
            </el-table-column>
            <el-table-column
              prop="address"
              label="地址">
            </el-table-column>
          </el-table>
          <el-pagination
          style="position: absolute; bottom: -250px;right: 250px;"
            background
            layout="prev, pager, next"
            :page-size="pageSize"
            :current-page.sync="currentPage"
            :total="tableData.length">
          </el-pagination>
        </div>
      </div>
      <div class="box-list-three">
        <div class="box-list-three-left1"  id="threeLeft2"></div>
        <div class="box-list-three-right1">
          <el-table
            :data="tableData1.slice((currentPage1-1)*pageSize1,currentPage1*pageSize1)"
            border
            style="width: 90%;margin: 40px;">
            <el-table-column
              prop="date"
              label="日期"
              width="180">
            </el-table-column>
            <el-table-column
              prop="name"
              label="姓名"
              width="180">
            </el-table-column>
            <el-table-column
              prop="address"
              label="地址">
            </el-table-column>
          </el-table>
          <el-pagination
          style="position: absolute; bottom: -770px;right: 370px;"
            background
            layout="prev, pager, next"
            :page-size="pageSize1"
            :current-page.sync="currentPage1"
            :total="tableData1.length">
          </el-pagination>
        </div>
      </div>
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
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }],
        tableData1: [{
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }]
      };
    },
    created(){

    },
    mounted() {
      //在浏览器宽度小于1200px时隐藏侧方导航栏菜单
      window.onresize = () => {
        if (document.documentElement.clientWidth < 1200) {
          this.isCollapse = true;
        }else {
          this.isCollapse = false;
        }
      };
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
            left: 'center',
            text: 'Large Ara Chart'
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

        let xAxisData = [];
        let data1 = [];
        let data2 = [];
        let data3 = [];
        let data4 = [];
        for (let i = 0; i < 10; i++) {
          xAxisData.push('Class' + i);
          data1.push(+(Math.random() * 2).toFixed(2));
          data2.push(+(Math.random() * 5).toFixed(2));
          data3.push(+(Math.random() + 0.3).toFixed(2));
          data4.push(+Math.random().toFixed(2));
        }
        var emphasisStyle = {
          itemStyle: {
            shadowBlur: 10,
            shadowColor: 'rgba(0,0,0,0.3)'
          }
        };
        option = {
          legend: {
            data: ['bar', 'bar2', 'bar3', 'bar4'],
            left: '10%'
          },
          brush: {
            toolbox: ['rect', 'polygon', 'lineX', 'lineY', 'keep', 'clear'],
            xAxisIndex: 0
          },
          toolbox: {
            feature: {
              magicType: {
                type: ['stack']
              },
              dataView: {}
            }
          },
          tooltip: {},
          xAxis: {
            data: xAxisData,
            name: 'X Axis',
            axisLine: { onZero: true },
            splitLine: { show: false },
            splitArea: { show: false }
          },
          yAxis: {},
          grid: {
            bottom: 100
          },
          series: [
            {
              name: 'bar',
              type: 'bar',
              stack: 'one',
              emphasis: emphasisStyle,
              data: data1
            },
            {
              name: 'bar2',
              type: 'bar',
              stack: 'one',
              emphasis: emphasisStyle,
              data: data2
            },
            {
              name: 'bar3',
              type: 'bar',
              stack: 'two',
              emphasis: emphasisStyle,
              data: data3
            },
            {
              name: 'bar4',
              type: 'bar',
              stack: 'two',
              emphasis: emphasisStyle,
              data: data4
            }
          ]
        };
        myChart.on('brushSelected', function (params) {
          var brushed = [];
          var brushComponent = params.batch[0];
          for (var sIdx = 0; sIdx < brushComponent.selected.length; sIdx++) {
            var rawIndices = brushComponent.selected[sIdx].dataIndex;
            brushed.push('[Series ' + sIdx + '] ' + rawIndices.join(', '));
          }
          myChart.setOption({
            title: {
              backgroundColor: '#333',
              text: 'SELECTED DATA INDICES: \n' + brushed.join('\n'),
              bottom: 0,
              right: '10%',
              width: 100,
              textStyle: {
                fontSize: 12,
                color: '#fff'
              }
            }
          });
        });

        option && myChart.setOption(option);
      },
      threeLeft2(){
        var chartDom = document.getElementById('threeLeft2');
        var myChart = echarts.init(chartDom);
        var option;

        option = {
          xAxis: {
            type: 'category',
            data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
          },
          yAxis: {
            type: 'value'
          },
          series: [
            {
              data: [
                120,
                {
                  value: 200,
                  itemStyle: {
                    color: '#a90000'
                  }
                },
                150,
                80,
                70,
                110,
                130
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
.el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 200px;
    min-height: 400px;
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
.box-list-three{
  display: flex;
}
.box-list-three-left{
  width: 600px;
  height: 500px;
  border: 1px solid black;
  margin: 10px;
}
.box-list-three-right{
  width: 1000px;
  height: 500px;
  border: 1px solid black;
  margin: 10px;
}
.box-list-three-left1{
  width: 800px;
  height: 500px;
  border: 1px solid black;
  margin: 10px;
}
.box-list-three-right1{
  width: 800px;
  height: 500px;
  border: 1px solid black;
  margin: 10px;
}
</style>
