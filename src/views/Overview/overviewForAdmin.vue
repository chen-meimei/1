<template>
  <div class="view5">
    <!-- 画图示例 -->
      <div class="view-layout">
          <div style="margin-right: 20px">
              <div id="patientType">
                  <p class="wenzi">患者类型分布</p>
                  <div id="patientTypeView"></div>
              </div>
              <div id="useAge">
                  <div style="display: flex;justify-content: space-between">
                      <p class="wenzi">使用年龄分布</p>
                      <div class="label-4-select">
                          <a-select id="select-in-overview" default-value="训练设备" style="width: 140px;padding: 15px 20px 0;color: #FF7F7F;font-weight:550;">
                              <a-select-option value="打印机">
                                  打印机
                              </a-select-option>
                              <a-select-option value="训练设备">
                                  训练设备
                              </a-select-option>
                              <a-select-option value="一代训练">
                                  一代训练
                              </a-select-option>
                              <a-select-option value="一代检查">
                                  一代检查
                              </a-select-option>
                          </a-select>
                      </div>
                  </div>

                  <div id="useAgeView"></div>
              </div>
          </div>
          <div class="view2">
              <div>
                  <p class="wenzi">新视锐全国分布</p>
                  <!--              style="margin: auto;width: 78%;height: 70%;"-->
                  <div id="mapTest" ></div>
              </div>
              <div id="dongtai">
                  <div style="margin: auto 0">
                      <p class="wenzi">实时动态</p>
                      <ul style="margin-top:calc((100vh - 68px) * 0.03);">
                          <li><span style="color: #000000">用户<span style="margin: 0 4px;color: #1079FA">张三</span>在<span style="margin: 0 4px;color: #1079FA">视力康复中心</span>进行了训练</span></li>
                          <li><span style="color: #000000">用户<span style="margin: 0 4px;color: #1079FA">张三</span>在<span style="margin: 0 4px;color: #1079FA">视力康复中心</span>进行了训练</span></li>
                          <li><span style="color: #000000">用户<span style="margin: 0 4px;color: #1079FA">张三</span>在<span style="margin: 0 4px;color: #1079FA">视力康复中心</span>进行了训练</span></li>
                          <!--                  <li><span style="margin: 0 4px;color: #0f19ff">用户</span>在<span style="margin: 0 4px;color: #0f19ff">视力康复中心</span>进行了训练</li>-->
                      </ul>
                  </div>
                  <div style="margin: auto 0">
                      <p class="wenzi1">总览</p>
                      <a-row style="margin:5px 30px 10px">
                          <a-col span="12" style="display: flex;justify-content: flex-start;">
                              <img src="../../assets/用户.png" alt="Big Boat" width="45" height="40" style="margin: 15px 10px 0 0">
                              <a-statistic title="累计注册用户" style="margin: auto 0; line-height:19px;"
                                           :value-style="{ 'margin-top': '1px' }"
                                           :value="1128">
                              </a-statistic>
                          </a-col>
                          <a-col span="12" style="display: flex;justify-content: flex-start;">
                              <img src="../../assets/图表-02.png" alt="Big Boat" width="50" height="45" style="margin: 15px 10px 0 0">
                              <a-statistic title="累计注册视光师"
                                           style="margin: auto 0; line-height:19px;"
                                           :value="1228">
                              </a-statistic>
                          </a-col>
                      </a-row>
                      <a-row style="margin: 10px 20px 0 30px">
                          <a-col span="12" style="display: flex;justify-content: flex-start;">
                              <img src="../../assets/图表-01.png" alt="Big Boat" width="45" height="40" style="margin: 15px 10px 0 0">
                              <a-statistic title="累计注册渠道"
                                           style="margin: auto 0; line-height:19px;"
                                           :value="1128">
                              </a-statistic>
                          </a-col>
                          <a-col span="12" style="display: flex;justify-content: flex-start;">
                              <img src="../../assets/图表-03.png" alt="Big Boat" width="45" height="40" style="margin: 15px 10px 0 0">
                              <a-statistic id="statistic" title="累计注册门店"
                                           style="margin: auto 0; line-height:19px;"
                                           :value="1228">
                              </a-statistic>
                          </a-col>
                      </a-row>
                  </div>
              </div>
          </div>
          <div>
              <div class="boxx3">
                  <p class="wenzi">用户增长趋势</p>
                  <div id="userGrowView"></div>
                  <p class="wenzi1">订单增长趋势</p>
                  <div id="goodsGrowView"></div>
              </div>
              <div id="goodsForm">
                  <p class="wenzi">订单转化情况</p>
                  <div id="goodsTransformView"></div>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
    import {Chart, registerShape} from '@antv/g2';
    import DataSet from '@antv/data-set';
    import ARow from "ant-design-vue/es/grid/Row";
    import ACol from "ant-design-vue/es/grid/Col";
export default {
    components: {ACol, ARow},
    data(){
    return{
        // height:document.documentElement.clientHeight,
        // width:document.documentElement.clientWidth,
        width:(screen.availWidth - 200-32),
        height:(screen.availHeight - 103-64-48),
        flagtest:1920,
        patientTypeBorder:{
            width1:undefined,
            height1:undefined,
        },
        usedAgeBorder:{
            width1:undefined,
            height1:undefined,
        },
        distributeBorder:{
            width1:undefined,
            height1:undefined,
        },
        userGrowBorder:{
            width1:undefined,
            height1:undefined,
        },
        goodsGrowBorder:{
            width1:undefined,
            height1:undefined,
        },
        goodsTransformBorder:{
            width1:undefined,
            height1:undefined,
        },

      //此处定义响应式数据
        basicColumnChartProp:{
            data:[
                { name: 'London', 月份: 'Jan.', 月均降雨量: 18.9 },
                { name: 'London', 月份: 'Feb.', 月均降雨量: 28.8 },
                { name: 'London', 月份: 'Mar.', 月均降雨量: 39.3 },
                { name: 'London', 月份: 'Apr.', 月均降雨量: 81.4 },
                { name: 'London', 月份: 'May', 月均降雨量: 47 },
                { name: 'London', 月份: 'Jun.', 月均降雨量: 20.3 },
                { name: 'Berlin', 月份: 'Jan.', 月均降雨量: 12.4 },
                { name: 'Berlin', 月份: 'Feb.', 月均降雨量: 23.2 },
                { name: 'Berlin', 月份: 'Mar.', 月均降雨量: 34.5 },
                { name: 'Berlin', 月份: 'Apr.', 月均降雨量: 99.7 },
                { name: 'Berlin', 月份: 'May', 月均降雨量: 52.6 },
                { name: 'Berlin', 月份: 'Jun.', 月均降雨量: 35.5 },
            ],
            container:'useAgeView',
        },
        basicTestProp:{
            data:[
                { feature: 'Battery', value: 0.22, phone: 'iPhone' },
                { feature: 'Brand', value: 0.28, phone: 'iPhone' },
                { feature: 'Contract', value: 0.29, phone: 'iPhone' },
                { feature: 'Design', value: 0.17, phone: 'iPhone' },
                { feature: 'Battery', value: 0.27, phone: 'Samsung' },
                { feature: 'Brand', value: 0.16, phone: 'Samsung' },
                { feature: 'Contract', value: 0.35, phone: 'Samsung' },
                { feature: 'Design', value: 0.13, phone: 'Samsung' },
                { feature: 'Battery', value: 0.26, phone: 'Nokia' },
                { feature: 'Brand', value: 0.1, phone: 'Nokia' },
                { feature: 'Contract', value: 0.3, phone: 'Nokia' },
                { feature: 'Design', value: 0.14, phone: 'Nokia' },
            ],
            container:'goodsGrowView'
        },
        basicTestOne:{
            data:[
                { type: '其他', value: 30 },
                { type: '远视', value: 27 },
                { type: '趋光参差', value: 20 },
                { type: '近视', value: 16 },
                { type: '生理性复视', value: 10 },
            ],
            container:'patientTypeView',
        },
        basicTestTwo:{
            data:[
                { time: '10:10', call: 4, people: 2 },
                { time: '10:15', call: 2, people: 3 },
                { time: '10:20', call: 13, people: 5 },
                { time: '10:25', call: 9, people: 1 },
                { time: '10:30', call: 5, people: 3 },
                { time: '10:35', call: 8, people: 1 },
                { time: '10:40', call: 13, people: 2 }
            ],
            container:'userGrowView'
        },
        basicTestThree:{
            data:[
                { type: '销售总额1', value: 34 },
                { type: '销售总额2', value: 85 },
                { type: '销售总额3', value: 103 },
                { type: '销售总额4', value: 142 },
                { type: '销售总额5', value: 251 },
            ],
            container:'goodsTransformView'
        },
    }
  },
  mounted(){
    //示例：绘制图表
      this.haha();
      this.testView1();
      this.drawLine1();
      this.testView4();
      this.testView2();
      this.testView();
      this.testView3();
  },
  methods:{
        haha(){
            // var adf = screen.availWidth;
            console.log(this.width);
            console.log(this.height);
            this.patientTypeBorder.width1=((this.width-40)*336/1153)-45;
            this.patientTypeBorder.height1=((this.height-15)*395/771)-65;
            this.usedAgeBorder.width1=((this.width-40)*336/1153)-50;
            this.usedAgeBorder.height1=((this.height-15)*376/771)-65;
            this.distributeBorder.width1=((this.width-40)*433/1153)-70;
            this.distributeBorder.height1=((this.height)*0.48)-65;
            this.userGrowBorder.width1=((this.width-40)*384/1153)-70;
            this.userGrowBorder.height1=((this.height-15)*250/773)-60;
            this.goodsGrowBorder.width1=((this.width-40)*384/1153)-70;
            this.goodsGrowBorder.height1=((this.height-15)*250/773)-60;
            this.goodsTransformBorder.width1=((this.width-40)*384/1153)-70;
            this.goodsTransformBorder.height1=((this.height-15)*229/773)-60;
            // if (this.flagtest <= 1900){
            //     this.patientTypeBorder.width1=300;
            //     this.patientTypeBorder.height1=330;
            //     this.usedAgeBorder.width1=300;
            //     this.usedAgeBorder.height1=300;
            //     this.distributeBorder.width1=385;
            //     this.distributeBorder.height1=319;
            //     this.userGrowBorder.width1=310;
            //     this.userGrowBorder.height1=210;
            //     this.goodsGrowBorder.width1=310;
            //     this.goodsGrowBorder.height1=210;
            //     this.goodsTransformBorder.width1=300;
            //     this.goodsTransformBorder.height1=160;
            // }
            // if (this.flagtest >= 1900) {
            //     this.patientTypeBorder.width1=435;
            //     this.patientTypeBorder.height1=340;
            //     this.usedAgeBorder.width1=435;
            //     this.usedAgeBorder.height1=334;
            //     this.distributeBorder.width1=500;
            //     this.distributeBorder.height1=350;
            //     this.userGrowBorder.width1=460;
            //     this.userGrowBorder.height1=215;
            //     this.goodsGrowBorder.width1=460;
            //     this.goodsGrowBorder.height1=215;
            //     this.goodsTransformBorder.width1=460;
            //     this.goodsTransformBorder.height1=180;
            // }
            // console.log(this.w1);
        },
      testView1(){
          const data2 = this.basicTestOne.data;
          let max = 0;
          data2.forEach(function(obj) {
              if (obj.value > max) {
                  max = obj.value;
              }
          });

// 自定义 other 的图形，增加两条线
          registerShape('interval', 'slice-shape', {
              draw(cfg, container) {
                  const points = cfg.points;
                  const origin = cfg.data;
                  const percent = origin.value / max;
                  const xWidth = points[2].x - points[1].x;
                  const width = xWidth * percent;
                  let path = [];
                  path.push(['M', points[0].x, points[0].y]);
                  path.push(['L', points[1].x, points[1].y]);
                  path.push(['L', points[0].x + width, points[2].y]);
                  path.push(['L', points[0].x + width, points[3].y]);
                  path.push('Z');
                  path = this.parsePath(path);
                  return container.addShape('path', {
                      attrs: {
                          fill: cfg.color,
                          path,
                      },
                  });
              },
          });
          const chart = new Chart({
              container: this.basicTestOne.container,
              width: this.patientTypeBorder.width1,
              height: this.patientTypeBorder.height1,
              autoFit:false,
          });
          chart.coordinate('theta', {
              radius: 0.8,
          });
          chart.data(data2);
          chart.tooltip({
              showTitle: false,
              showMarkers: false,
          });
          chart.legend('type',{
              position: 'bottom',
              autoWrap:false,
              flipPage: false,
              maxWidth:290,
              itemWidth:70,
              itemSpacing: 7,
              offsetX:10,
              marker:{
                  symbol:'square',
              }
          });
          chart
              .interval()
              .adjust('stack')
              .position('value')
              .color('type',['#46A6FF','#A8EC00','#FFD100','#FF9F16','#FF6161'])
              .shape('slice-shape');

          chart.interaction('element-active');

          chart.render();
      },
      drawLine1(){
          const data = this.basicColumnChartProp.data;
          const chart = new Chart({
              container: this.basicColumnChartProp.container,
              width: this.usedAgeBorder.width1,
              height: this.usedAgeBorder.height1,
              autoFit:false,
          });
          chart.data(data);
          chart.scale('月均降雨量', {
              min: 0,
              max: 110,
          });
          // chart.scale({
          //     people: {
          //         min: 0,
          //         max: 6,
          //     },
          // });
          chart.tooltip({
              showMarkers: false,
              shared: true,
          });
          chart.interval().position('月份*月均降雨量')
              .color('name').adjust([
              {
                  type: 'dodge',
                  marginRatio: 0,
              },
          ]);
          chart.interaction('active-region');
          chart.render();
      },
      testView4(){
          fetch('https:/g2.antv.vision/zh/examples/data/china-provinces.geo.json')
              .then(res => res.json())
              .then(mapData => {
                  const chart = new Chart({
                      container: 'mapTest',
                      autoFit: false,
                      width:this.distributeBorder.width1,
                      height: this.distributeBorder.height1,
                      padding: [5, 5]
                  });
                  chart.tooltip({
                      showTitle: false,
                      showMarkers: false,
                      shared: true,
                  });
                  // 同步度量
                  chart.scale({
                      longitude: {
                          sync: true
                      },
                      latitude: {
                          sync: true
                      }
                  });
                  chart.axis(false);
                  chart.legend(false);

                  // 绘制地图背景
                  const ds = new DataSet();
                  const worldMap = ds.createView('back')
                      .source(mapData, {
                          type: 'GeoJSON'
                      });
                  const worldMapView = chart.createView();
                  worldMapView.data(worldMap.rows);
                  worldMapView.tooltip(false);
                  worldMapView.polygon().position('longitude*latitude').style({
                      fill: '#9df2ff',
                      stroke: '#ffffff',
                      lineWidth: 1
                  });

                  // 可视化用户数据
                  const userData = [
                      { name: '新疆维吾尔自治区', value: 86.8 },
                      { name: '西藏自治区', value: 106.3 },
                      { name: '云南省', value: 94.7 },
                      { name: '湖南省', value: 98 },
                      { name: '吉林省', value: 98.4 },
                  ];
                  const userDv = ds.createView()
                      .source(userData)
                      .transform({
                          geoDataView: worldMap,
                          field: 'name',
                          type: 'geo.region',
                          as: ['longitude', 'latitude']
                      })
                      .transform({
                          type: 'map',
                          callback: obj => {
                              obj.trend = (obj.value > 100) ? '男性更多' : '女性更多';
                              return obj;
                          }
                      });
                  const userView = chart.createView();
                  userView.data(userDv.rows);
                  userView.scale({
                      trend: {
                          alias: '每100位女性对应的男性数量'
                      }
                  });
                  userView.polygon()
                      .position('longitude*latitude')
                      .color('trend', ['#F51D27', '#0A61D7'])
                      .tooltip('name*trend')
                      .style({
                          fillOpacity: 0.85
                      })
                      .animate({
                          leave: {
                              animation: 'fade-out'
                          }
                      });
                  userView.interaction('element-active');

                  chart.render();
              });
      },
      testView2(){
          const data1 = this.basicTestTwo.data;
          const chart = new Chart({
              container: this.basicTestTwo.container,
              width: this.userGrowBorder.width1,
              height: this.userGrowBorder.height1,
              autoFit:false,
          });
          chart.data(data1);
          chart.scale({
              people: {
                  min: 0,
                  max: 6,
              },
          });
          chart.axis('people',{
              grid:null,
          });
          chart.axis('time', {
              grid: {
                  type: 'line',
                  lineStyle: {
                      stroke: '#d9d9d9',
                      lineWidth: 1,
                  },
                  align: 'center' // 网格顶点从两个刻度中间开始
              }
          });
          chart.tooltip({
              shared: true,
          });
          chart.line()
              .position('time*people')
              .color('#FF1655')
              .size(3)
              .shape('smooth');
          chart
              .area()
              .position('time*people')
              .color('#fdafbe')
              .shape('smooth');

          chart.interaction('active-region');
          chart.removeInteraction('legend-filter'); // 自定义图例，移除默认的分类图例筛选交互
          chart.render();
      },
      testView(){
          const data1 = this.basicTestProp.data;
          const chart = new Chart({
              container: this.basicTestProp.container,
              width: this.goodsGrowBorder.width1,
              height: this.goodsGrowBorder.height1,
              autoFit:false,
          });
          chart.data(data1);
          chart.line().position('feature*value').color('phone');
          chart.render();
      },
      testView3(){
          const data1 = this.basicTestThree.data;
          const chart = new Chart({
              container: this.basicTestThree.container,
              width: this.goodsTransformBorder.width1,
              height: this.goodsTransformBorder.height1,
              autoFit:false,
          });
          chart.data(data1);
          chart.scale('value',{
              nice: true
          });
          chart.axis('type', {
              title: null,
              tickLine: null,
              line: null,
          });

          chart.axis('value', {
              label: null,
              title: null,
              // title: {
              //     offset: 30,
              //     style: {
              //         fontSize: 12,
              //         fontWeight: 300,
              //     },
              // },
          });
          chart.legend(false);
          chart.coordinate().transpose();
          chart
              .point()
              .adjust('stack')
              .position('type*value')
              .color('type')
              .size(5)
              .shape('circle');
          chart
              .interval()
              .position('type*value')
              .color('type')
              .size(6)
              .label('value', {
                  style: {
                      fill: '#8d8d8d',
                  },
                  offset: 10,
              });
          chart.interaction('element-active');
          chart.render();
      },
  }
}
</script>
<style scoped>
    /*.view5{position: fixed;overflow-x: auto;}*/
.view-layout{
    /*border-style: dotted;*/
    /*height:100%;*/
    /*width:100%;*/
    /*min-width: 755px;*/
    box-sizing: border-box;
    margin:auto 0;
    background-color:rgba(235,239,241,1);
    display: flex;
    justify-content: space-between;
    overflow-x: auto;

}
ul {list-style-type:none;}
ul li::before {
    content: "●";
    color: #1079FA;
    position: relative;
    margin-right: 5px;
    font-size: 22px;
}
ul li{
    height:calc((100vh - 68px) * 0.04);
    font-weight:bold;
    /*font-size: calc((100vh - 68px) * 0.02);*/
}
    /*!*1024*567*!*/
    /*@media only screen and (max-device-width: 1200px){*/
    /*    .wenzi{*/
    /*        height:17px;*/
    /*        !*margin-bottom: 50px;*!*/
    /*        padding: 10px 20px 0;*/
    /*        font-size:15px;*/
    /*        line-height:25px;*/
    /*        font-weight:600;*/
    /*        color:rgba(0,0,0,1);*/
    /*    }*/
    /*    .wenzi1{*/
    /*        height:17px;*/
    /*        padding: 1px 20px 0;*/
    /*        font-size:15px;*/
    /*        line-height:25px;*/
    /*        font-weight:600;*/
    /*        color:rgba(0,0,0,1);*/
    /*    }*/
    /*    #patientType{*/
    /*        height:252px;*/
    /*        width:220px;*/
    /*        margin-bottom: 13px;*/
    /*        border-radius:6px;*/
    /*        background-color: rgba(255,255,255,1);*/
    /*    }*/
    /*    #useAge{*/
    /*        height:242px;*/
    /*        width:220px;*/
    /*        border-radius:6px;*/
    /*        background-color: rgba(255,255,255,1);*/
    /*    }*/
    /*    .boxx3{*/
    /*        !*width:384px;*!*/
    /*        !*height:544px;*!*/
    /*        width:336px;*/
    /*        height:348px;*/
    /*        display: flex;*/
    /*        flex-direction: column;*/
    /*        justify-content: space-around;*/
    /*        !*margin-bottom: 2%;*!*/
    /*        margin-bottom: 13px;*/
    /*        border-radius:6px;*/
    /*        background-color: rgba(255,255,255,1);*/
    /*    }*/
    /*    #goodsForm {*/
    /*        width: 336px;*/
    /*        height: 146px;*/
    /*        !*height:32%;*!*/
    /*        border-radius: 6px;*/
    /*        background-color: rgba(255, 255, 255, 1);*/
    /*    }*/
    /*    .view2{*/
    /*        display:flex;*/
    /*        flex-direction:column;*/
    /*        !*justify-content: space-between;*!*/
    /*        !*width: 36%;*!*/
    /*        width: 378px;*/
    /*        height: 312px;*/
    /*        margin-right: 20px;*/
    /*        !*height:100%;*!*/
    /*        border-radius:6px;*/
    /*        background-color: rgba(255,255,255,1);*/
    /*    }*/
    /*    #dongtai{margin: auto 0;height: 295px;*/
    /*        display: flex;flex-direction: column;*/
    /*        justify-content: space-between}*/
    /*    #useAgeView{width: 90%;margin:10px auto 0;}*/
    /*    #mapTest{width: 320px;margin: 0 auto;}*/
    /*    #userGrowView{width: 86%;margin:10px auto 0;}*/
    /*    #goodsGrowView{width: 86%;margin:0 auto 0;}*/
    /*    #goodsTransformView{width: 86%;margin:20px auto 0;}*/
    /*}*/
    @media only screen and (max-device-width: 1100px){
        .wenzi{
            height:17px;
            /*margin-bottom: 50px;*/
            padding: 10px 20px 0;
            font-size:15px;
            line-height:25px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        .wenzi1{
            height:17px;
            padding: 1px 20px 0;
            font-size:15px;
            line-height:25px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        #patientType{
            height:252px;
            width:294px;
            margin-bottom: 13px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #useAge{
            height:242px;
            width:294px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        .boxx3{
            /*width:384px;*/
            /*height:544px;*/
            width:336px;
            height:348px;
            display: flex;
            flex-direction: column;
            justify-content: space-around;
            /*margin-bottom: 2%;*/
            margin-bottom: 13px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #goodsForm {
            width: 336px;
            height: 146px;
            /*height:32%;*/
            border-radius: 6px;
            background-color: rgba(255, 255, 255, 1);
        }
        .view2{
            display:flex;
            flex-direction:column;
            /*justify-content: space-between;*/
            /*width: 36%;*/
            width: 378px;
            height: 505px;
            margin-right: 20px;
            /*height:100%;*/
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #dongtai{margin: auto 0;height: 295px;
            display: flex;flex-direction: column;
            justify-content: space-between}
        #useAgeView{width: 90%;margin:10px auto 0;}
        #mapTest{width: 320px;margin: 0 auto;}
        #userGrowView{width: 86%;margin:10px auto 0;}
        #goodsGrowView{width: 86%;margin:0 auto 0;}
        #goodsTransformView{width: 86%;margin:20px auto 0;}
    }
    /*1280*720*/
    @media only screen and (min-device-width: 1200px) and (min-device-height: 700px){
        .wenzi{
            height:17px;
            /*margin-bottom: 50px;*/
            padding: 10px 20px 0;
            font-size:15px;
            line-height:25px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        .wenzi1{
            height:17px;
            padding: 1px 20px 0;
            font-size:15px;
            line-height:25px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        #patientType{
            height:252px;
            width:294px;
            margin-bottom: 13px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #useAge{
            height:242px;
            width:294px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        .boxx3{
            /*width:384px;*/
            /*height:544px;*/
            width:336px;
            height:348px;
            display: flex;
            flex-direction: column;
            justify-content: space-around;
            /*margin-bottom: 2%;*/
            margin-bottom: 13px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #goodsForm {
            width: 336px;
            height: 146px;
            /*height:32%;*/
            border-radius: 6px;
            background-color: rgba(255, 255, 255, 1);
        }
        .view2{
            display:flex;
            flex-direction:column;
            /*justify-content: space-between;*/
            /*width: 36%;*/
            width: 378px;
            height: 505px;
            margin-right: 20px;
            /*height:100%;*/
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #dongtai{margin: auto 0;height: 295px;
            display: flex;flex-direction: column;
            justify-content: space-between}
        #useAgeView{width: 90%;margin:10px auto 0;}
        #mapTest{width: 320px;margin: 0 auto;}
        #userGrowView{width: 86%;margin:10px auto 0;}
        #goodsGrowView{width: 86%;margin:0 auto 0;}
        #goodsTransformView{width: 86%;margin:20px auto 0;}
    }
    /*1280*800*/
    @media only screen and (min-device-width: 1200px) and (min-device-height: 780px){
        .wenzi{
            height:17px;
            /*margin-bottom: 50px;*/
            padding: 10px 20px 0;
            font-size:15px;
            line-height:25px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        .wenzi1{
            height:17px;
            padding: 1px 20px 0;
            font-size:15px;
            line-height:25px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        #patientType{
            height:275px;
            width:294px;
            margin-bottom: 13px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #useAge{
            height:264px;
            width:294px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        .boxx3{
            /*width:384px;*/
            /*height:544px;*/
            width:336px;
            height:379px;
            display: flex;
            flex-direction: column;
            justify-content: space-around;
            /*margin-bottom: 2%;*/
            margin-bottom: 13px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #goodsForm {
            width: 336px;
            height: 160px;
            /*height:32%;*/
            border-radius: 6px;
            background-color: rgba(255, 255, 255, 1);
        }
        .view2{
            display:flex;
            flex-direction:column;
            /*justify-content: space-between;*/
            /*width: 36%;*/
            width: 378px;
            height: 550px;
            margin-right: 20px;
            /*height:100%;*/
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #dongtai{margin: auto 0;height: 295px;
            display: flex;flex-direction: column;
            justify-content: space-between}
        #useAgeView{width: 90%;margin:10px auto 0;}
        #mapTest{width: 320px;margin: 0 auto;}
        #userGrowView{width: 86%;margin:10px auto 0;}
        #goodsGrowView{width: 86%;margin:0 auto 0;}
        #goodsTransformView{width: 86%;margin:20px auto 0;}
    }
    /*1366*768*/
    @media only screen and (min-device-width: 1300px) {
        .wenzi{
            height:20px;
            /*margin-bottom: 50px;*/
            padding: 15px 23px 0;
            font-size:18px;
            line-height:29px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        .wenzi1{
            height:20px;
            padding: 1px 23px 0;
            font-size:18px;
            line-height:29px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        #patientType{
             height:276px;
             width:319px;
             margin-bottom: 13px;
             border-radius:6px;
             background-color: rgba(255,255,255,1);
         }
        #useAge{
            height:265px;
            width:319px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        .boxx3{
            /*width:384px;*/
            /*height:544px;*/
            width:364px;
            height:381px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            /*margin-bottom: 2%;*/
            margin-bottom: 13px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #goodsForm {
            width: 364px;
            height: 160px;
            /*height:32%;*/
            border-radius: 6px;
            background-color: rgba(255, 255, 255, 1);
        }
        .view2{
            display:flex;
            flex-direction:column;
            /*justify-content: space-between;*/
            /*width: 36%;*/
            width: 410px;
            height: 553px;
            margin-right: 20px;
            /*height:100%;*/
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #useAgeView{width: 90%;margin:10px auto 0;}
        #mapTest{width: 390px;margin: 0 auto;}
        #userGrowView{width: 86%;margin:10px auto 0;}
        #goodsGrowView{width: 86%;margin:10px auto 0;}
        #goodsTransformView{width: 86%;margin:30px auto 0;}
    }
    /*1440*900*/
    @media only screen and (min-device-width: 1400px) {
        .wenzi{
            height:20px;
            /*margin-bottom: 50px;*/
            padding: 15px 23px 0;
            font-size:18px;
            line-height:29px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        .wenzi1{
            height:20px;
            padding: 1px 23px 0;
            font-size:18px;
            line-height:29px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }#patientType{
        height:324px;
        width:336px;
        margin-bottom: 13px;
        border-radius:6px;
        background-color: rgba(255,255,255,1);
    }
    #useAge{
        height:305px;
        width:336px;
        border-radius:6px;
        background-color: rgba(255,255,255,1);
    }
    .boxx3{
        /*width:384px;*/
        /*height:544px;*/
        width:384px;
        height:473px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        /*margin-bottom: 2%;*/
        margin-bottom: 13px;
        border-radius:6px;
        background-color: rgba(255,255,255,1);
    }
    #goodsForm {
        width: 384px;
        height: 157px;
        /*height:32%;*/
        border-radius: 6px;
        background-color: rgba(255, 255, 255, 1);
    }
    .view2{
        display:flex;
        flex-direction:column;
        /*justify-content: space-between;*/
        /*width: 36%;*/
        width: 433px;
        height: 642px;
        margin-right: 20px;
        /*height:100%;*/
        border-radius:6px;
        background-color: rgba(255,255,255,1);
    }
    #useAgeView{width: 90%;margin:10px auto 0;}
    #mapTest{width: 390px;margin: 0 auto;}
    #userGrowView{width: 86%;margin:10px auto 0;}
    #goodsGrowView{width: 86%;margin:10px auto 0;}
    #goodsTransformView{width: 86%;margin:30px auto 0;}
}
    /*1680*1050*/
    @media only screen and (min-device-width: 1640px) {
    ul li{
        font-size: 15px;
    }
        .wenzi{
            height:20px;
            /*margin-bottom: 50px;*/
            padding: 15px 23px 0;
            font-size:18px;
            line-height:29px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        .wenzi1{
            height:20px;
            padding: 1px 23px 0;
            font-size:18px;
            line-height:29px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
    #patientType{
        height:399px;
        width:410px;
        margin-bottom: 13px;
        border-radius:6px;
        background-color: rgba(255,255,255,1);
    }
    #useAge{
        height:383px;
        width:410px;
        border-radius:6px;
        background-color: rgba(255,255,255,1);
    }
    .boxx3{
        /*width:384px;*/
        /*height:544px;*/
        width:468px;
        height:548px;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        /*margin-bottom: 2%;*/
        margin-bottom: 13px;
        border-radius:6px;
        background-color: rgba(255,255,255,1);
    }
    #goodsForm {
        width: 468px;
        height: 231px;
        /*height:32%;*/
        border-radius: 6px;
        background-color: rgba(255, 255, 255, 1);
    }
    .view2{
        display:flex;
        flex-direction:column;
        justify-content: space-between;
        /*width: 36%;*/
        width: 529px;
        height: 795px;
        margin-right: 20px;
        /*height:100%;*/
        border-radius:6px;
        background-color: rgba(255,255,255,1);
    }
    #dongtai{margin: auto 0;height: 380px;
        display: flex;flex-direction: column;
        justify-content: space-between}
    #useAgeView{width: 90%;margin:10px auto 0;}
    #mapTest{width: 477px;margin: auto;}
    #userGrowView{width: 86%;margin:10px auto 0;}
    #goodsGrowView{width: 86%;margin:10px auto 0;}
    #goodsTransformView{width: 86%;margin:30px auto 0;}
}
    /*1920*1080*/
    @media only screen and (min-device-width: 1900px) and (min-device-height: 1000px){
        .wenzi{
            height:20px;
            /*margin-bottom: 50px;*/
            padding: 15px 23px 0;
            font-size:18px;
            line-height:29px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        .wenzi1{
            height:20px;
            padding: 1px 23px 0;
            font-size:18px;
            line-height:29px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        #patientType{
        height:413px;
        width:480px;
        margin-bottom: 15px;
        border-radius:6px;
        background-color: rgba(255,255,255,1);
    }
    #useAge{
        height:396px;
        width:480px;
        border-radius:6px;
        background-color: rgba(255,255,255,1);
    }
    .boxx3{
        /*width:384px;*/
        /*height:544px;*/
        width:540px;
        height:569px;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        /*margin-bottom: 2%;*/
        margin-bottom: 15px;
        border-radius:6px;
        background-color: rgba(255,255,255,1);
    }
    #goodsForm {
        width: 540px;
        height: 240px;
        /*height:32%;*/
        border-radius: 6px;
        background-color: rgba(255, 255, 255, 1);
    }
    .view2{
        /*box-sizing: border-box;*/
        display:flex;
        flex-direction:column;
        justify-content: flex-start;
        width: 618px;
        height: 825px;
        margin-right: 20px;
        /*height:100%;*/
        border-radius:6px;
        background-color: rgba(255,255,255,1);
    }
    #dongtai{margin: auto 0;height: 410px;
        display: flex;flex-direction: column;justify-content: space-between}
    #useAgeView{width: 90%;margin:10px auto 0;}
    #mapTest{width: 557px;margin: auto;}
    #userGrowView{width: 86%;margin:10px auto 0;}
    #goodsGrowView{width: 86%;margin:10px auto 0;}
    #goodsTransformView{width: 86%;margin:30px auto 0;}
}
    /*1920*1200*/
    @media only screen and (min-device-width: 1900px) and (min-device-height: 1150px){
        .wenzi{
            height:20px;
            /*margin-bottom: 50px;*/
            padding: 15px 23px 0;
            font-size:18px;
            line-height:29px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        .wenzi1{
            height:20px;
            padding: 1px 23px 0;
            font-size:18px;
            line-height:29px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        #patientType{
            height:472px;
            width:480px;
            margin-bottom: 15px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #useAge{
            height:454px;
            width:480px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        .boxx3{
            /*width:384px;*/
            /*height:544px;*/
            width:540px;
            height:652px;
            display: flex;
            flex-direction: column;
            justify-content: space-around;
            /*margin-bottom: 2%;*/
            margin-bottom: 15px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #goodsForm {
            width: 540px;
            height: 274px;
            /*height:32%;*/
            border-radius: 6px;
            background-color: rgba(255, 255, 255, 1);
        }
        .view2{
            /*box-sizing: border-box;*/
            display:flex;
            flex-direction:column;
            justify-content: flex-start;
            width: 618px;
            height: 945px;
            margin-right: 20px;
            /*height:100%;*/
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #dongtai{margin: auto 0;height: 430px;
            display: flex;flex-direction: column;justify-content: space-between}
        #useAgeView{width: 90%;margin:10px auto 0;}
        #mapTest{width: 557px;margin: auto;}
        #userGrowView{width: 86%;margin:10px auto 0;}
        #goodsGrowView{width: 86%;margin:10px auto 0;}
        #goodsTransformView{width: 86%;margin:30px auto 0;}
    }
    /*2560×1600*/
    @media only screen and (min-device-width: 2000px) {
        ul li{
            font-size: 15px;
        }
        .wenzi{
            height:20px;
            /*margin-bottom: 50px;*/
            padding: 20px 28px 0;
            font-size:28px;
            line-height:29px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        .wenzi1{
            height:20px;
            padding: 1px 28px 0;
            font-size:28px;
            line-height:29px;
            font-weight:600;
            color:rgba(0,0,0,1);
        }
        #patientType{
            height:673px;
            width:666px;
            margin-bottom: 27px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #useAge{
            height:645px;
            width:666px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        .boxx3{
            /*width:384px;*/
            /*height:544px;*/
            width:762px;
            height:928px;
            display: flex;
            flex-direction: column;
            justify-content: space-around;
            /*margin-bottom: 2%;*/
            margin-bottom: 27px;
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #goodsForm {
            width: 762px;
            height: 390px;
            /*height:32%;*/
            border-radius: 6px;
            background-color: rgba(255, 255, 255, 1);
        }
        .view2{
            display:flex;
            flex-direction:column;
            justify-content: space-between;
            /*width: 36%;*/
            width: 859px;
            height: 1345px;
            margin-right: 20px;
            /*height:100%;*/
            border-radius:6px;
            background-color: rgba(255,255,255,1);
        }
        #dongtai{margin: auto 0;height: 560px;
            display: flex;flex-direction: column;
            justify-content: space-between}
        #useAgeView{width: 90%;margin:10px auto 0;}
        #mapTest{width: 795px;margin: auto;}
        #userGrowView{width: 86%;margin:10px auto 0;}
        #goodsGrowView{width: 86%;margin:10px auto 0;}
        #goodsTransformView{width: 86%;margin:30px auto 0;}
    }
    
    /*#test2{*/
/*    display: flex;*/
/*    align-items: center;*/
/*    width:calc((100vw - 200px) * 0.26);*/
/*    height:calc((100vh - 68px) * 0.39);*/
/*    margin: auto;*/
/*}*/
/*#test3{*/
/*    width:calc((100vw - 200px) * 0.29);*/
/*    height:calc((100vh - 68px) * 0.27);*/
/*}*/
/*#test1{*/
/*    width:calc((100vw - 200px) * 0.29);*/
/*    height:calc((100vh - 68px) * 0.27);*/
/*}*/
/*#test4{*/
/*    width:calc((100vw - 200px) * 0.29);*/
/*    height:calc((100vh - 68px) * 0.24);*/
/*}*/
/*#test5{*/
/*    width:calc((100vw - 200px) * 0.25);*/
/*    height:calc((100vh - 68px) * 0.37);*/
/*    margin: auto;*/
/*}*/
/*#dongtai{*/
/*    height:calc((100vh - 68px) * 0.25);*/
/*}*/
/*#example{*/
/*    display: flex;*/
/*    align-items: center;*/
/*    width:calc((100vw - 200px) * 0.25);*/
/*    height:calc((100vh - 68px) * 0.40);*/
/*    margin: auto;*/
/*}*/
/*#goodsForm{*/
/*    !*width:384px;*!*/
/*    !*height:228px;*!*/
/*    !*width:99%;*!*/
/*    height:32%;*/
/*    border-radius:6px;*/
/*    background-color: rgba(255,255,255,1);*/
/*}*/
/*#useAge{*/
/*    display: flex;*/
/*    flex-direction: column;*/
/*    justify-content: space-between;*/
/*    height:50%;*/
/*    border-radius:6px;*/
/*    background-color: rgba(255,255,255,1);*/
/*}*/
/*.boxx3{*/
/*    !*width:384px;*!*/
/*    !*height:544px;*!*/
/*    !*width:99%;*!*/
/*    height:67%;*/
/*    margin-bottom: 2%;*/
/*    border-radius:6px;*/
/*    background-color: rgba(255,255,255,1);*/
/*}*/
/*.view2{*/
/*    display:flex;*/
/*    flex-direction:column;*/
/*    justify-content: space-between;*/
/*    width: 36%;*/
/*    margin-right: 1%;*/
/*    height:100%;*/
/*    border-radius:6px;*/
/*    background-color: rgba(255,255,255,1);*/
/*}*/
</style>






