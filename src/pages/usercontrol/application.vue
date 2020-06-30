<template>
  <div id="Subject">
    <a-Card :style="{'display':'flex','justify-content':'flex-end','margin-bottom':'10px'}">
      <a-input
      v-model="searchPhone"
      placeholder="Input a number"
      :max-length="25"
      :style="{'width': '200px','margin-right':'10px'}"
    />
    <a-input
      v-model="searchNick"
      placeholder="Input a nick"
      :max-length="25"
      style="width: 200px"
    />
    <a-button type="primary" @click="search">查詢</a-button>
    </a-Card>
    <a-card>
      <a-table :columns="columns" :data-source="data" :row-selection="rowSelection">
        <template slot="operation" slot-scope="text, record">
          <div class="Flex">
          <a href="/usercontrol/authorization" :style="{'margin-right':'10px'}" type="link">授权管理</a>
           </div>
        </template>
      </a-table>
    </a-card>

  </div>
</template>
<script>

const columns = [
  {
    title: '序号',
    dataIndex: 'erial',
    key: 'erial'
  },
  {
    title: '头像',
    dataIndex: 'avatars',
    key: 'avatars',
    width: '12%'
  },
  {
    title: '昵称',
    dataIndex: 'name',
    // width: '30%',
    key: 'name'
  },
  {
    title: '手机号',
    dataIndex: 'phoneNumer',
    // width: '30%',
    key: 'phoneNumer'
  },
  {
    title: 'VIP授权情况',
    dataIndex: 'VIP',
    // width: '30%',
    key: 'VIP'
  },
  {
    title: '申请时间',
    dataIndex: 'risgerTime',
    // width: '30%',
    key: 'risgerTime'
  },
  {
    title: '申请科目',
    dataIndex: 'subject',
    // width: '30%',
    key: 'subject'
  },
  {
    title: '申请留言',
    dataIndex: 'note',
    // width: '30%',
    key: 'note',
  },
  {
    title: '操作',
    dataIndex: 'operation',
    scopedSlots: { customRender: 'operation' }
  }
]

const data = [
  {
    key: 1,
    name: 'John Brown sr.',
    age: 60,
    address: 'New York No. 1 Lake Park',
  },
  {
    key: 2,
    name: 'Joe Black',
    age: 32,
    address: 'Sidney No. 1 Lake Park'
  }
]

const rowSelection = {
  onChange: (selectedRowKeys, selectedRows) => {
    console.log(`selectedRowKeys: ${selectedRowKeys}`, 'selectedRows: ', selectedRows)
  },
  onSelect: (record, selected, selectedRows) => {
    console.log(record, selected, selectedRows)
  },
  onSelectAll: (selected, selectedRows, changeRows) => {
    console.log(selected, selectedRows, changeRows)
  }
}
export default {
  data() {
    return {
      data,
      columns,
      rowSelection,
      searchPhone:'',
      searchNick:'',
    }
  },
  methods: {
    // search 查詢
    search(){
      let searchInfo = {
        searchPhone:this.searchPhone,
        searchNick:this.searchNick
      }
      console.log(searchInfo)
    }
  },
  components:{

  }
}
</script>
<style >
#Subject .buttonBox {
  margin-bottom: 10px;
  display: flex;
}
#Subject .ant-table-thead > tr > th {
  color: white;
  background: #4a90e2 !important;
}
.Flex{
  display: flex;
}
</style>
