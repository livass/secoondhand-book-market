<template>
 <el-tabs :tab-position="tabPosition" style="height: 200px;">
    <el-tab-pane label="图书查看">
       <el-table
    :data="tableData1"
    style="width: 100%"
    :row-class-name="tableRowClassName">
    <el-table-column
      prop="date"
      label="书名"
      width="180">
    </el-table-column>
    <el-table-column
      prop="name"
      label="卖家"
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="价格"
      width="180">
    </el-table-column>
     <el-table-column
      prop="pp"
      label="介绍">
    </el-table-column>
    <el-table-column
      fixed="right"
      label="操作"
      width="180">
      <template slot-scope="scope">
        <el-button @click="handleClick(scope.row)" type="text" size="small">查看详情</el-button>
        <el-button type="text" size="small">购买</el-button>
      </template>
    </el-table-column>
  </el-table>
    </el-tab-pane>
    <el-tab-pane label="已购买图书">
       <el-table
    :data="tableData2"
    style="width: 100%"
    :row-class-name="tableRowClassName">
    <el-table-column
      prop="date"
      label="书名"
      width="180">
    </el-table-column>
    <el-table-column
      prop="name"
      label="卖家"
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="价格"
      width="180">
    </el-table-column>
     <el-table-column
      prop="pp"
      label="介绍">
    </el-table-column>
    <el-table-column
      fixed="right"
      label="操作"
      width="180">
      <template slot-scope="scope">
        <el-button @click="handleClick1(scope.row,scope.$index)" type="text" size="small">评价</el-button>
        <el-button type="text" size="small">退款</el-button>
      </template>
    </el-table-column>
  </el-table>
    </el-tab-pane>
    <el-tab-pane label="上传图书">
      <!--上传图片-->
      <el-upload
    class="avatar-uploader"
    action="url+'post'"
    :show-file-list="false"
    :on-success="handleAvatarSuccess"
    :before-upload="beforeAvatarUpload">
    <img v-if="imageUrl" :src="imageUrl" class="avatar">
    <i v-else class="el-icon-plus avatar-uploader-icon"></i>
</el-upload>
    <!--文本框相关数据-->
    <br><br>
    <el-input
  type="textarea"
  autosize
  placeholder="请输入书名"
  v-model="textarea1">
</el-input>
<div style="margin: 20px 0;"></div>
<el-input
  type="textarea"
  :autosize="{ minRows: 2, maxRows: 4}"
  placeholder="请简要介绍一下自己的图书"
  v-model="textarea2">
</el-input>
<br><br>
<el-input v-model="price" placeholder="请输入价格(元)"></el-input>
<br><br>
<el-button type="primary" round>发布信息</el-button>
    </el-tab-pane>
  </el-tabs>
</template>

<script>
  export default {
    data() {
      return {
        tabPosition: 'top',
        imageUrl: '',
        textarea1:'',
        textarea2:'',
        price:'',
       tableData1: [{
          date: 'c++',
          name: '王小虎',
          address: '30',
          pp:'欢迎购买',
        }, {
          date: 'c#',
          name: '王小虎',
          address: '50',
          pp:'价格可议',
        }, {
          date: 'web',
          name: '王小虎',
          address: '30',
          pp:'666666',
        }, {
          date: 'java',
          name: '王小虎',
          address: '25.2',
          pp:'java',
        }],
        tableData2: [{
          date: 'go',
          name: '王小虎',
          address: '60',
          pp:'很棒',
        }], 
      };
    },
     methods: {
        // eslint-disable-next-line no-unused-vars
        tableRowClassName({row, rowIndex}) {
        if (rowIndex === 1) {
          return 'warning-row';
        } else if (rowIndex === 3) {
          return 'success-row';
        }
        return '';
      },
      // eslint-disable-next-line no-unused-vars
      handleClick1(row,index){
        location.href='#/admin'
      },
      handleAvatarSuccess(res, file) {
        this.imageUrl = URL.createObjectURL(file.raw);
      },
      beforeAvatarUpload(file) {
        const isJPG = file.type === 'image/jpeg';
        const isLt2M = file.size / 1024 / 1024 < 2;
        if (!isJPG) {
          this.$message.error('上传图书图片只能是 JPG 格式!');
        }
        if (!isLt2M) {
          this.$message.error('上传图书图片大小不能超过 2MB!');
        }
        return isJPG && isLt2M;
      }
    }
  };
</script>

<style>
.el-table .warning-row {
    background: oldlace;
  }

  .el-table .success-row {
    background: #f0f9eb;
  }
  .avatar-uploader .el-upload {
    border: 1px dashed #d9d9d9;
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }
  .avatar-uploader .el-upload:hover {
    border-color: #409EFF;
  }
  .avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    line-height: 178px;
    text-align: center;
  }
  .avatar {
    width: 178px;
    height: 178px;
    display: block;
  }
</style>