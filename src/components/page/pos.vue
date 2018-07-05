<template>
  <div class="pos">
    <el-row>
      <el-col :span='7' class="posA" id="posB">
        <el-tabs>
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border style="width=100%">
              <el-table-column prop="goodsName" label="商品名称"></el-table-column>
              <el-table-column prop="count" label="量" width="50"></el-table-column>
              <el-table-column prop="price" label="价格" width="70"></el-table-column>
              <el-table-column label="操作" width="100" fixed="right">
                <template slot-scope="scope">
            <el-button type="text" label="shanchu" size="small">删除</el-button>
            <el-button type="text" size="small">增加</el-button>
 
                </template>
              </el-table-column>
                
            </el-table>
            <div class="div-btn">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger">删除</el-button>
              <el-button type="success">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单">挂单</el-tab-pane>
          <el-tab-pane label="外卖">外卖</el-tab-pane>

          
        </el-tabs>
      </el-col>

      <el-col :span="17">
        <div class="often-goods">
          <div class="title">常用商品</div>
          <div class="often-goods-list">
            <ul>
              <li v-for="goods in oftenGoods">
                <span>{{goods.goodsName}}</span>
                <span class="o-price">￥{{goods.price}}元</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="goods-type">
          <el-tabs>
            <el-tab-pane label=汉堡>
              <div>
<ul class='cookList'>
    <li v-for="goods in type0Goods">
        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
        <span class="foodName">{{goods.goodsName}}</span>
        <span class="foodPrice">￥{{goods.price}}元</span>
    </li>
</ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label=小食>小食</el-tab-pane>
            <el-tab-pane label=饮料>饮料</el-tab-pane>
            <el-tab-pane label=套餐>套餐</el-tab-pane>
            </el-tabs>
        </div>

      </el-col>
    </el-row>
  </div>
</template>
 
<script>
import axios from 'axios';
export default {
  name: 'pos',
  data(){
   return{
     tableData:[{
          
          goodsName: '可口可乐',
          price: 8,
          count:1
        }, {
          
          goodsName: '香辣鸡腿堡',
          price: 15,
          count:1
        }, {
         
          goodsName: '爱心薯条',
          price: 8,
          count:1
        }, {
         
          goodsName: '甜筒',
          price: 8,
          count:1
        }],
        oftenGoods:[],
      type0Goods:[],
      type1Goods:[],
      type2Goods:[],
      type3Goods:[]
   }
  },
  created:function() {
      axios.get('http://jspang.com/DemoApi/oftenGoods.php')
      .then(reponse=>{
      //console.log(reponse);
      this.oftenGoods=reponse.data;
      })
      .catch(error=>{
          //console.log(error);
          alert('网络错误，不能访问');
      })
  },
  created:function() {
      axios.get('http://jspang.com/DemoApi/typeGoods.php')
      .then(reponse=>{
    //   console.log(reponse);
      this.type0Goods=reponse.data[0];
      this.type1Goods=reponse.data[1];
      this.type2Goods=reponse.data[2];
      this.type3Goods=reponse.data[3];
      })
      .catch(error=>{
          //console.log(error);
          alert('网络错误，不能访问');
      })
  },
  mounted:function(){
    var posBHeight=document.body.clientHeight;
    console.log(posBHeight)
    document.getElementById('posB').style.height=posBHeight+"px";
  }
}
</script>
<style scoped>
 .posA{
   background-color: #f9fafc;
   border-right:1px solid #c0ccda;
   }
 .div-btn{
  margin-top: 15px;
  text-align: center;
}
 .title{
   height: 20px;
   border-bottom:1px solid #D3dce6;
   background-color: #f9fafc;
   padding: 10px;
   text-align: left; 
 }
 .often-goods-list ul li{
    list-style: none;
    float: left;
    border: 1px solid #E5e9f2;
    padding: 10px;
    margin: 10px;
    background-color: #fff;
 }
 .o-price{
   color: #58b7ff;
 }
 .goods-type{
   clear: both;
 }
.cookList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auto;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;
 
   }
   .cookList li span{
       
        display: block;
        float:left;
   }
   .foodImg{
       width: 40%;
   }
   .foodName{
       font-size: 18px;
       padding-left: 10px;
       color:brown;
 
   }
   .foodPrice{
       font-size: 16px;
       padding-left: 10px;
       padding-top:10px;
   }
</style>