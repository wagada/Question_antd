<template>
  <div id="pagesmanagement">
    <a-Card :style="{'margin-bottom':'10px'}" class="radius">
      <!-- 行业选择 -->
      <a-select style="width: 200px" @change="industryChange" placeholder="行业">
        <a-select-option value="互联网">互联网</a-select-option>
        <a-select-option value="教育">教育</a-select-option>
        <a-select-option value="雷霆嘎巴">雷霆嘎巴</a-select-option>
      </a-select>
      <!-- 科目选择 -->
      <a-select
        class="radius"
        :style="{'margin-left':'10px'}"
        style="width: 200px"
        @change="subjectChange"
        placeholder="科目"
      >
        <a-select-option value="毛概">毛概</a-select-option>
        <a-select-option value="高数">高数</a-select-option>
        <a-select-option value="C语言">C语言</a-select-option>
      </a-select>
    </a-Card>
    <!-- 表格 -->
    <a-Card class="radius">
      <a-table :columns="columns" :data-source="data">
        <!-- 状态插槽 -->
        <template slot="status" slot-scope="status">
          <div :style="{'text-align':'center'}">
            <a :style="{'color':'#1990FF','margin-right':'10px'}">试用</a>
            <a :style="{'color':'#FAAE13','margin-right':'10px'}">VIP</a>
          </div>
        </template>
        <!-- 操作插槽 -->
        <template slot="opction" slot-scope="opction">
          <div :style="{'text-align':'center'}">
            <a :style="{'color':'#DCDCDC','margin-right':'10px'}">下架</a>
            <a :style="{'color':'#FAAE13','margin-right':'10px'}">VIP</a>
            <a :style="{'color':'#63C83B','margin-right':'10px'}">上架</a>
            <a :style="{'color':'#1990FF','margin-right':'10px'}">试用</a>
          </div>
        </template>
      </a-table>
    </a-Card>
  </div>
</template>

<script>
const columns = [
  {
    title: '名称',
    dataIndex: 'name',
    scopedSlots: { customRender: 'name' }
  },
  {
    title: '状态修改时间',
    className: 'column-money',
    dataIndex: 'money'
  },
  {
    title: '上下架状态',
    dataIndex: 'address'
  },
  {
    title: '试用/vip状态',
    dataIndex: 'status',
    scopedSlots: { customRender: 'status' }
  },
  {
    title: 'opction',
    scopedSlots: { customRender: 'opction' }
  }
]

const data = [
  {
    key: '1',
    name: 'John Brown',
    money: '￥300,000.00',
    address: 'New York No. 1 Lake Park'
  },
  {
    key: '2',
    name: 'Jim Green',
    money: '￥1,256,000.00',
    address: 'London No. 1 Lake Park'
  },
  {
    key: '3',
    name: 'Joe Black',
    money: '￥120,000.00',
    address: 'Sidney No. 1 Lake Park'
  }
]
export default {
  data() {
    return {
      data,
      columns
    }
  },
  methods: {
    industryChange(value) {
      console.log(value)
    },
    subjectChange(value) {
      console.log(value)
    }
  }
}
</script>

<style>
#pagesmanagement .radius {
  border-radius: 4px;
}
#pagesmanagement .ant-select-selection {
  border-radius: 4px;
}
#pagesmanagement .ant-table {
  border-left: 1px solid rgba(220, 220, 220, 1);
  border-right: 1px solid rgba(220, 220, 220, 1);
  border-radius: 4px;
}
#pagesmanagement .ant-table th {
  text-align: center;
  height: 50px;
  background: rgba(25, 144, 255, 1);
  opacity: 1;
  color: white;
}
#pagesmanagement .ant-table td {
  text-align: center;
}
</style>