<template>
  <div>
    <el-container style="height: 500px; border: 1px solid #eee" direction="horizontal">
      <el-aside width="200px" style="background-color: rgb(238, 241, 246)"> </el-aside>

      <el-container>
        <el-header style="text-align: right; font-size: 12px"> </el-header>
        <el-main>
          <i class="el-icon-edit"></i>
          <h3>这些按钮</h3>
          <div>
            <el-row :gutter="5">
              <el-button size="small">默认按钮</el-button>
              <el-button type="primary" size="mini">主要按钮</el-button>
              <el-button type="success">成功按钮</el-button>
              <el-button type="info">信息按钮</el-button>
              <el-button type="warning">警告按钮</el-button>
              <el-button type="danger">危险按钮</el-button>
            </el-row>
            <el-row :gutter="5">
              <el-button plain>朴素按钮</el-button>
              <el-button type="primary" plain disabled>主要按钮</el-button>
              <el-button type="success" plain>成功按钮</el-button>
              <el-button type="info" plain>信息按钮</el-button>
              <el-button type="warning" plain>警告按钮</el-button>
              <el-button type="danger" plain>危险按钮</el-button>
            </el-row>
            <el-row :gutter="5">
              <el-button round>圆角按钮</el-button>
              <el-button type="primary" round>主要按钮</el-button>
              <el-button type="success" round>成功按钮</el-button>
              <el-button type="info" round>信息按钮</el-button>
              <el-button type="warning" round>警告按钮</el-button>
              <el-button type="danger" round>危险按钮</el-button>
            </el-row>
            <el-row>
              <el-button icon="el-icon-search" circle></el-button>
              <el-button type="primary" icon="el-icon-edit" circle></el-button>
              <el-button type="success" icon="el-icon-check" circle></el-button>
              <el-button type="info" icon="el-icon-message" circle></el-button>
              <el-button type="warning" icon="el-icon-star-off" circle></el-button>
              <el-button type="danger" icon="el-icon-delete" circle></el-button>
            </el-row>
          </div>
          <h3>还有这些按钮</h3>
          <div>
            <el-button-group>
              <el-button type="primary" icon="el-icon-arrow-left">上一页</el-button>
              <el-button type="primary">下一页<i class="el-icon-arrow-right el-icon--right"></i></el-button>
            </el-button-group>
            <el-button-group>
              <el-button type="primary" icon="el-icon-edit"></el-button>
              <el-button type="primary" icon="el-icon-share"></el-button>
              <el-button type="primary" icon="el-icon-delete"></el-button>
              <el-button type="primary" :loading="true">加载中</el-button>
            </el-button-group>
          </div>
          <h3>单选框</h3>
          <div>
            <el-radio v-model="radio" label="1">备选项</el-radio>
            <el-radio v-model="radio" label="2">备选项</el-radio>
          </div>
          <h3>输入框（可清空）</h3>
          <div class="shuru">
            <el-input placeholder="请输入内容" v-model="input10" clearable> </el-input>
          </div>
          <h3>服务端搜索输入框</h3>
          <div>
            <el-autocomplete
              v-model="state4"
              :fetch-suggestions="querySearchAsync"
              placeholder="请输入内容"
              @select="handleSelect"
            ></el-autocomplete>
          </div>
          <h3>number</h3>
          <div>
            <InNumber @numberChange="numberChange" :min="1" :max="20"></InNumber>
          </div>
          <h3>分页控件</h3>
          <div>
            <el-pagination background layout="prev, pager, next" :total="200"> </el-pagination>
          </div>
          <h3>日期控件</h3>
          <div><DatePicker></DatePicker></div>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import InNumber from '@/components/InNumber'
import DatePicker from '@/components/Datepicker'
export default {
  data() {
    const item = {
      date: '2016-05-02',
      name: '王小虎',
      address: '上海市普陀区金沙江路 1518 弄'
    }
    return {
      tableData: Array(20).fill(item),
      radio: '1',
      input10: '',
      restaurants: [],
      state4: '',
      timeout: null,
      numbers: 1
    }
  },
  methods: {
    loadAll() {
      return [
        { value: '三全鲜食（北新泾店）', address: '长宁区新渔路144号' },
        { value: 'Hot honey 首尔炸鸡（仙霞路）', address: '上海市长宁区淞虹路661号' },
        { value: '新旺角茶餐厅', address: '上海市普陀区真北路988号创邑金沙谷6号楼113' },
        { value: '泷千家(天山西路店)', address: '天山西路438号' },
        { value: '胖仙女纸杯蛋糕（上海凌空店）', address: '上海市长宁区金钟路968号1幢18号楼一层商铺18-101' }
      ]
    },
    querySearchAsync(queryString, cb) {
      var restaurants = this.restaurants
      var results = queryString ? restaurants.filter(this.createStateFilter(queryString)) : restaurants

      clearTimeout(this.timeout)
      this.timeout = setTimeout(() => {
        cb(results)
      }, 3000 * Math.random())
    },
    createStateFilter(queryString) {
      return state => {
        return state.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0
      }
    },
    handleSelect(item) {
      console.log(item)
    },
    numberChange(value) {
      console.log(value)
    }
  },
  mounted() {
    this.restaurants = this.loadAll()
  },
  components: {
    InNumber,
    DatePicker
  }
}
</script>

<style lang="scss" scoped="scoped">
.el-header {
  background-color: #b3c0d1;
  color: #333;
  line-height: 60px;
}

.el-aside {
  color: #333;
}
.el-main {
  .el-row {
    margin-bottom: 20px;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .shuru {
    width: 170px;
    height: 40px;
  }
}
</style>
