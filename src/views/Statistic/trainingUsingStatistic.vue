<template>
  <div class="subpage-layout">
    <div class="subpage-title">
      训练使用
    </div>
    <div class="subpage-content">
      <!-- 请在此处填充内容 -->
      <div class="form-area" style="width:100%" >
        <a-row style="display:flex;justify-content:space-between;margin-bottom:15px">
          <a-col :span="4">
            <a-form-model-item 
              label="渠道" 
              :labelCol="{span:4}"
              :wrapperCol="{offset:1,span:16}">
              <a-input v-model="channel"/>
            </a-form-model-item>
          </a-col>
          <a-col :span="4">
            <a-form-model-item 
              label="门店"
              :labelCol="{span:4}"
              :wrapperCol="{offset:1,span:16}">
              <a-input v-model="store"/>
            </a-form-model-item>
          </a-col>
          <a-col :span="4">
            <a-form-model-item 
              label="用户"
              :labelCol="{span:4}"
              :wrapperCol="{offset:1,span:16}">
              <a-input v-model="user"/>
            </a-form-model-item>
          </a-col>
          <a-col :span="5">
            <a-form-model-item 
              label="视光师"
              :labelCol="{span:5}"
              :wrapperCol="{offset:1,span:14}">
              <a-input v-model="optometrist"/>
            </a-form-model-item>
          </a-col>
          <a-col :span="6">
            <a-form-model-item 
              label="设备编号"
              :labelCol="{span:5}"
              :wrapperCol="{offset:1,span:14}">
              <a-input v-model="deviceId"/>
            </a-form-model-item>
          </a-col>
        </a-row>
        <a-row style="display:flex;justify-content:space-between;margin-bottom:15px">
          <a-col :span="4">
            <a-form-model-item 
              label="时间"
              labelAlign="left"
              :labelCol="{span:4}"
              :wrapperCol="{offset:1,span:19}">
              <a-date-picker 
                style="width:100%" 
                placeholder="请选择日期" 
                v-model="useTime"/>
            </a-form-model-item>
          </a-col>
          <a-col :span="8" style="display:flex;align-items:center">
            <div style="margin-left:10%;width:55%;display:flex;justify-content:space-around;align-items:center">
              <a-button type="primary" @click="search">搜索</a-button>
              <a-button type="primary" @click="reset">重置</a-button>
              <a-button style="color:white;background-color:#faad14;">导出</a-button>
            </div>
          </a-col>
          <a-col :span="12">
          </a-col>
        </a-row>
      </div>
      <div class="table-area" style="width:100%;margin-top:20px">
        <a-table style="width:100%;height:100%" 
          :columns="columns" 
          :data-source="data" 
          :pagination="pagination"
          bordered>
          <template slot="customRender" slot-scope="text,record,index,column">
            <span v-if="searching && form[column.dataIndex].trim() !== ''">
              <template
                v-for="(fragment, i) in text
                  .toString()
                  .split(new RegExp(`(${form[column.dataIndex].trim()})`, 'i'))"
              >
                <mark
                  v-if="fragment.toLowerCase() === form[column.dataIndex].trim().toLowerCase()"
                  :key="i"
                  class="highlight"
                  >{{ fragment }}</mark
                >
                <template v-else>{{ fragment }}</template>
              </template>
            </span>
            <template v-else>
              {{ text }}
            </template>
          </template>
          <span slot="action">
            <a-button type="primary" 
              style="margin:2px 20px 2px 0"
              @click="showModal">
              开始筛查
            </a-button>
            <a-button type="primary">报告</a-button>
          </span>
        </a-table>
        <div style="width:250px;position:relative;top:-80px;">
          <span>每页显示</span>
          <a-input style="width:35px;height:30px;text-align:center;outline:none;margin:0 3px;padding:0 2px" 
            v-model="pageSize" 
            defaultValue="10"
            @blur="changePageSize"
            @pressEnter="changePageSize"
            />
          <span>条记录</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const columns = [
  {
    title: '序号',
    dataIndex: 'number',
    key: 'number',
    align:'center'
  },
  {
    title: '用户',
    dataIndex: 'user',
    key: 'user',
    align:'center',
    scopedSlots:{
      customRender:'customRender'
    }
  },
  {
    title: '渠道',
    dataIndex: 'channel',
    key: 'channel',
    align:'center',
    scopedSlots:{
      customRender:'customRender'
    }
  },
  {
    title: '门店',
    key: 'store',
    dataIndex: 'store',
    align:'center',
    scopedSlots:{
      customRender:'customRender'
    }
  },
  {
    title: '设备编号',
    dataIndex: 'deviceId',
    key: 'deviceId',
    align:'center',
    scopedSlots:{
      customRender:'customRender'
    }
  },
  {
    title: '视光师',
    key: 'optometrist',
    dataIndex: 'optometrist',
    align:'center',
    scopedSlots:{
      customRender:'customRender'
    }
  },
  {
    title: '使用时间',
    key: 'useTime',
    dataIndex: 'useTime',
    align:'center',
    scopedSlots:{
      customRender:'customRender'
    }
  }
];
const time = new Date();
let formatTime = function(time){
  let year = time.getFullYear();
  let month = time.getMonth();
  month = month < 10 ? `0${month}` : month;
  let date = time.getDate();
  date = data < 10 ? `0${date}` : date;
  let hour = time.getHours();
  let min = time.getMinutes();
  let sec = time.getSeconds();
  return `${year}/${month}/${date} ${hour}:${min}:${sec}`;
}
const data = [
  {
    key:1,
    user:'0001',
    nickName:'Shine',
    channel:'优丫优直营渠道',
    store:'爱尔眼科',
    deviceId:'0001',
    optometrist:'Lily',
    useTime:formatTime(time)
  },
  {
    key:2,
    user:'0001',
    nickName:'Shine',
    channel:'优丫优直营渠道',
    store:'爱尔眼科',
    deviceId:'0002',
    optometrist:'Lily',
    useTime:formatTime(time)
  },
  {
    key:3,
    user:'0003',
    nickName:'Liam',
    channel:'新视直营渠道',
    store:'光明眼科',
    deviceId:'0003',
    optometrist:'Heily',
    useTime:formatTime(time)
  },
  {
    key:4,
    user:'0003',
    nickName:'Liam',
    channel:'新视直营渠道',
    store:'光明眼科',
    deviceId:'0004',
    optometrist:'Heily',
    useTime:formatTime(time)
  },
  {
    key:5,
    user:'0002',
    nickName:'Bob',
    channel:'健康直营渠道',
    store:'优眼眼科',
    deviceId:'0003',
    optometrist:'Heily',
    useTime:formatTime(time)
  },
  {
    key:6,
    user:'0005',
    nickName:'Zheng',
    channel:'健康直营渠道',
    store:'优眼眼科',
    deviceId:'0007',
    optometrist:'Alice',
    useTime:formatTime(time)
  },
  {
    key:7,
    user:'0002',
    nickName:'Bob',
    channel:'快销直营渠道',
    store:'哲文眼科',
    deviceId:'0007',
    optometrist:'Alice',
    useTime:formatTime(time)
  },
  {
    key:8,
    user:'0002',
    nickName:'Bob',
    channel:'快销直营渠道',
    store:'哲文眼科',
    deviceId:'0007',
    optometrist:'Alice',
    useTime:formatTime(time)
  },
  {
    key:9,
    user:'0008',
    nickName:'Silence',
    channel:'快销直营渠道',
    store:'哲文眼科',
    deviceId:'0009',
    optometrist:'Alice',
    useTime:formatTime(time)
  },
 {
    key:10,
    user:'0008',
    nickName:'Silence',
    channel:'快销直营渠道',
    store:'哲文眼科',
    deviceId:'0009',
    optometrist:'Alice',
    useTime:formatTime(time)
  },
  {
    key:11,
    user:'0008',
    nickName:'Silence',
    channel:'快销直营渠道',
    store:'哲文眼科',
    deviceId:'0009',
    optometrist:'Alice',
    useTime:formatTime(time)
  },
  {
    key:12,
    user:'0008',
    nickName:'Silence',
    channel:'快销直营渠道',
    store:'哲文眼科',
    deviceId:'0009',
    optometrist:'Alice',
    useTime:formatTime(time)
  },
  {
    key:13,
    user:'0008',
    nickName:'Silence',
    channel:'快销直营渠道',
    store:'哲文眼科',
    deviceId:'0009',
    optometrist:'Alice',
    useTime:formatTime(time)
  },
];
function addNumber(data){
  for(let i = 0;i<data.length;i++){
    data[i].number = i + 1;
  }
}
addNumber(data);
export default {
  data(){
    return {
      data,
      columns,
      channel:'',
      store:'',
      user:'',
      optometrist:'',
      deviceId:'',
      useTime:'',
      form:{
        channel:'',
        store:'',
        user:'',
        optometrist:'',
        deviceIde:'',
        useTime:'',
      },
      searching:false,
      pageSize:10,
      pagination:{pageSize:10},
    }
  },
  methods:{
    //点击搜索按钮
    search:function(){
      this.form.channel = this.channel;
      this.form.store = this.store;
      this.form.user = this.user;
      this.form.optometrist = this.optometrist;
      this.form.deviceId = this.deviceId;
      this.form.useTime = this.useTime ? this.useTime.format('YYYY/MM/DD') : '';
      let index = ['channel','store','user','optometrist','deviceId','useTime'];
      let search_data = data, i = 0;
      while(i < index.length){
        let target = this.form[index[i]].trim();
        if( target !== ''){
          search_data = search_data.filter(value => {
            return value[index[i]].indexOf(target) > -1;
          })
        }
        i++;
      }
      this.data = search_data;
      this.searching = true;
    },
    reset(){
      this.searching = false;
      this.data = data;
      this.form = {
        channel:'',
        store:'',
        user:'',
        optometrist:'',
        deviceIde:'',
        useTime:'',
      };
      this.channel='';
      this.store='';
      this.user='';
      this.optometrist='';
      this.deviceId='';
      this.useTime='';
    },
    //改变表格每页显示数据条数
    changePageSize:function(e){
      e.target.blur();
      this.pagination = {pageSize: parseInt(this.pageSize)};
    },
    //控制对话框显示
    showModal() {
      this.visible = true;
    },
    //对话框点击开始按钮
    handleOk() {
      //！！！此处代码有待修改！！！
      this.confirmLoading = true;
      setTimeout(() => {
        this.visible = false;
        this.confirmLoading = false;
      }, 2000);
    },
    //对话框点击取消按钮
    handleCancel() {
      this.visible = false;
    },
  }
}
</script>

<style scoped>
.ant-row::before, .ant-row::after{
  content:none;
}
.highlight {
  background-color: rgb(253, 245, 1);
  padding: 0px;
}
</style>