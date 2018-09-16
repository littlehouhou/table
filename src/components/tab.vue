<template>
  <div class="warp">
    <div class="header">危险化学品企业安全风险分级评价-企业自评</div>
    <el-button type="primary" class="addEvaluation">新增企业年度自评</el-button>
    <el-table :data="records">
      <el-table-column prop="date" label="年度" width="100">
      </el-table-column>
      <el-table-column prop="name" label="企业名称" width="180">
      </el-table-column>
      <el-table-column prop="authority" label="管理隶属" width="120">
      </el-table-column>
      <el-table-column prop="grade" label="企业级别" width="120">
      </el-table-column>
      <el-table-column label="企业自评等级">
        <el-table-column prop="score" label="自评得分" width="120">
        </el-table-column>
        <el-table-column prop="ygrade" label="对应等级" width="120">
        </el-table-column>
      </el-table-column>
      <el-table-column prop="coucheck" label="县（市、区）安监局复核" width="200">
      </el-table-column>
      <el-table-column prop="citycheck" label="市（州）安监局复核" width="200">
      </el-table-column>
      <el-table-column prop="procheck" label="省安监局复核" width="120">
      </el-table-column>
      <el-table-column prop="state" label="状态" :filters="[
        {text: '暂存', value: 0},
        {text: '县安监局复核中', value: 1},
        {text: '市安监局复核中', value: 2},
        {text: '省安监局复核中', value: 3},
        {text: '县/市/省安监局复核退回', value: 4},
        {text: '县/市/省安监局复核完成', value: 5}
      ]"
      :filter-method="filterState">
      <template slot-scope="scope">
        <p>{{ states[scope.row.state].name }}</p>
      </template>
      </el-table-column>
      <el-table-column label="操作" width="400" prop="operation">
        <template slot-scope="scope">
          <div class="handle">
            <el-button
              v-if="states[scope.row.state].value === 'tempStorage' || states[scope.row.state].value === 'back'"
              size="mini"
                type="primary"
              @click="handleEdit(scope.$index, scope.row)">上报</el-button>
            <el-button
              v-if="states[scope.row.state].value === 'tempStorage' || states[scope.row.state].value === 'back'"
              size="mini"
                type="primary"
              @click="handleEdit(scope.$index, scope.row)">查看与修改</el-button>
            <el-button
              v-if="states[scope.row.state].value === 'review' || states[scope.row.state].value === 'done'"
              size="mini"
                type="primary"
              @click="handleEdit(scope.$index, scope.row)">查看详表</el-button>
            <el-button
              v-if="states[scope.row.state].value === 'done'"
              size="mini"
                type="primary"
              @click="handleEdit(scope.$index, scope.row)">导出与打印</el-button>
            <el-button
                v-if="states[scope.row.state].value === 'tempStorage' || states[scope.row.state].value === 'back'"
              size="mini"
              type="danger"
              @click="handleDelete(scope.$index, scope.row)">删除</el-button>
          </div>
        </template>
      </el-table-column>   
  </el-table>
</div>
</template>

<script>
  export default {
    data() {
      return {
        states: [
          {
            name: '暂存',
            value: 'tempStorage',
          },
          {
            name: '县安监局复核中',
            value: 'review',
          },
          {
            name: '市安监局复核中',
            value: 'review',
          },
          {
            name: '省安监局复核中',
            value: 'review',
          },
          {
            name: '县/市/省安监局复核退回',
            value: 'back',
          },
          {
            name: '县/市/省安监局复核完成',
            value: 'done',
          },
        ],
        records: [{
          date: '2018',
          name: '****',
          authority: '***安监局',
          grade: '县直管企业',
          score: '85',
          ygrade: '黄色（B级）',
          coucheck: '',
          citycheck: '',
          procheck: '',
          operation: '',
          state: 0,
        }, {
          date: '2018',
          name: '****',
          authority: '***安监局',
          grade: '县直管企业',
          score: '85',
          ygrade: '黄色（B级）',
          coucheck: '橙色（C级）',
          citycheck: '',
          procheck: '',
          operation: '',
          state: 1,
        }, {
          date: '2018',
          name: '****',
          authority: '***安监局',
          grade: '县直管企业',
          score: '85',
          ygrade: '黄色（B级）',
          coucheck: '橙色（C级）',
          citycheck: '橙色（C级）',
          procheck: '',
          operation: '',
          state: 2,
        }, {
          date: '2018',
          name: '****',
          authority: '***安监局',
          grade: '县直管企业',
          score: '85',
          ygrade: '黄色（B级）',
          coucheck: '橙色（C级）',
          citycheck: '橙色（C级）',
          procheck: '',
          operation: '',
          state: 3,
        }, {
          date: '2018',
          name: '****',
          authority: '***安监局',
          grade: '县直管企业',
          score: '85',
          ygrade: '黄色（B级）',
          coucheck: '',
          citycheck: '',
          procheck: '',
          operation: '',
          state: 4,
        }, {
          date: '2018',
          name: '****',
          authority: '***安监局',
          grade: '县直管企业',
          score: '85',
          ygrade: '黄色（B级）',
          coucheck: '橙色（C级）',
          citycheck: '橙色（C级）',
          procheck: '',
          operation: '',
          state: 5,
        }]
      }
    },
      methods: {
        filterState(value, row, column) {
          const property = column['property'];
          return row[property] === value;
        }
      }
  }
</script>

<style>
  .warp {
    width: 96%;
    margin: 20px auto 0;
  }
  
  .header {
    height: 30px;
    line-height: 30px;
    border-bottom: 1px solid #ccc;
  }
  
  .el-table thead {
    color: #090909;
    font-size: 14px;
  }
  
  .el-table thead.is-group th {
    background: #f3f7f600;
  }
  
  .el-table td,
  .el-table th {
    padding: 5px 0;
    text-align: center;
  }
  
  .el-table--border th {
    border-right: 1px solid #090909;
  }
  
  .el-table--border td {
    border-right: 0;
  }
  
  .el-table th.is-leaf {
    border-bottom: 1px solid #090909;
  }
  
  .addEvaluation {
    margin: 16px 0;
    float: right;
    box-shadow: 0 0 14px rgba(0, 0, 0, 0.2);
  }
  
  .el-button {
    min-width: 100px;
    border-radius: 4px;
  }
  
  .el-button--primary {
    background-color: #1b99cf;
    border: 1px solid #1b99cf;
  }
  
  .el-button--danger {
    background-color: #fe0200;
    border: 1px solid #fe0200;
  }
  
  .handle {
    text-align: right;
  }

  .el-table {
    border: 1px solid #090909;
  }

  .el-table__header-wrapper thead th:nth-child(5) {
    border-bottom: 1px solid #090909;
  }
</style>