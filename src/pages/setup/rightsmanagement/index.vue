<template>
  <div id="rightsmanagement">
    <a-Card class="Flex" :style="{'margin-bottom':'10px','border-radius':'6px'}">
      <!-- <a-button class="roles">添加角色</a-button> -->
      <Addroles/>
      <a-input-search
        placeholder="input search text"
        enter-button="查询"
        @search="onSearch"
        style="width:250px;margin-left:700px"
      />
    </a-Card>
    <a-Card :style="{'border-radius':'6px'}">
      <a-table :columns="columns" :data-source="data">
        <template slot="opction" slot-scope="opction">
          <div :style="{'text-align':'center'}">
            <a :style="{'color':'#1990FF','margin-right':'10px'}">编辑</a>
            <a :style="{'color':'#FF5757'}">禁用</a>
          </div>
        </template>
      </a-table>
    </a-Card>
  </div>
</template>
<script>
import Addroles from './components/Addroles'
const columns = [
  {
    title: '角色',
    dataIndex: 'name',
    scopedSlots: { customRender: 'name' }
  },
  {
    title: '权限',
    className: 'column-money',
    dataIndex: 'money'
  },
  {
    title: '创建时间',
    dataIndex: 'address'
  },
  {
    title: '操作',
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
    onSearch(value) {
      console.log(value)
    }
  },
  components:{
      Addroles,
  }
}
</script>
<style>
#rightsmanagement .roles {
  width: 100px;
  height: 32px;
  background: rgba(25, 144, 255, 1);
  opacity: 1;
  border-radius: 4px;
  color: white;
}
#rightsmanagement .Flex .ant-card-body {
  display: flex;
  align-content: center;
}
#rightsmanagement .ant-btn-primary {
  background: #1990ff;
  border-radius: 4px;
}
#rightsmanagement .ant-table-body {
  border-left: 1px solid rgba(220, 220, 220, 1);
  border-right: 1px solid rgba(220, 220, 220, 1);
  border-radius:4px;
}
#rightsmanagement .ant-table-body th{
    text-align: center;
    background:rgba(25,144,255,1);
    color: white;
}
#rightsmanagement .ant-table-body td{
    text-align: center;
}
</style>