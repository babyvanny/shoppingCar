<template>
    <div class="hello">
       
      <table id="cartTable">
          <thead>
              <tr>
                  <th>
                      <label><input class="check-all check" type="checkbox"   v-model="checkall" @click="checkallbnt"> 全选</label>
                  </th>
                  <th>商品</th>
                  <th>单价</th>
                  <th>数量</th>
                  <th>小计</th>
                  <th>操作</th>
              </tr>
          </thead>
          <tbody>
              <tr v-for="(item,index) in goodList">
                  <td class="checkbox"><input type="checkbox" class="check-one check" v-model="item.sb1" @click="sbbnt">
                  </td>
                  <td class="goods">
                      <img src=""><span>{{ item.goods }}</span>
                  </td>
                
                  <td class="price">
                      <span>{{ item.price }}.00</span>
                  </td>
                  <td class="goods-number">
                      <span class="reduce" @click="redNum(index)">➖</span>
                      <input type="text" v-model="item.num"><span class="add" @click="addNum(index)">➕</span>
                  </td>
                  <td class="subtotal">
                      <span>{{ item.subtotal }}.00</span>
                  </td>
                  <td class="operation">
                      <span class="delete" @click="run(index)">删除</span>
                  </td>
              </tr>
            

          </tbody>
      </table>
      <div class="foot" id="foot">
          <label class="fl select-all">
              <input type="checkbox" class="check-all check" v-model="checkall" @click="checkallbnt">全选
          </label>
          <a class="fl delete" id="delete-all" href="javascript:'">删除</a>
          <div class="fr closing">结算</div>
          <div class="fr total">
          合计：￥<span id="total-price">{{totalprice}}.00</span>
          </div>  
          <div class="fr selected" id="selected">已选商品
            <span id="selectedTital">0</span>
            <span class="arrow up">up</span>
            <span class="arrow down">down</span>
          </div>
          <div class="selected-view">
            <div id="selected-viewlist"></div>
            <span class="arrow"><span>.</span></span>
          </div>
    </div> 
    </div>
</template>

<script>
export default {
    name: 'hello',
    data () {
        return {
            msg: 'Welcome to Your Vue.js App',
            checkall:true,     
            goodList: [
                {
                    goods: '笔记本',
                    price: 12000,
                    num: 1,
                    subtotal:12000,
                    sb1:true
                },
                {
                    goods: '口红',
                    price: 200,
                    num: 1,
                    subtotal:200,
                    sb1:true
                },
                {
                    goods: '电脑桌',
                    price: 360,
                    num: 1,
                    subtotal:360,
                    sb1:true
                }
            ]
        }
    },
    methods:{
       
        addNum:function(index){
            this.goodList[index].num++
            this.goodList[index].subtotal = this.goodList[index].num*this.goodList[index].price
           
        },
        redNum:function(index){
            if(this.goodList[index].num==1){
                this.goodList[index].num==1
            }else{
                this.goodList[index].num--
                this.goodList[index].subtotal = this.goodList[index].num*this.goodList[index].price
            }

            
        },
        run: function (index) {
            this.goodList.splice( index, 1)
        },
        checkallbnt:function(){
            for(var i = 0;i<this.goodList.length;i++){
                if(this.checkall==true){
                    this.goodList[i].sb1=true
                }else{
                    this.goodList[i].sb1=false
                }
            }
                
        },
        sbbnt:function () {
           
            // for(var i = 0;i<this.goodList.length;i++){
            //     if(this.goodList[i].sb1==false){
                   
            //         this.checkall=false
            //     }
            // }
          
            var checkall = true
            for(var i = 0;i<this.goodList.length;i++){
                checkall = checkall && this.goodList[i].sb1
            }
            this.checkall = checkall
        }
    },
    computed: {
        totalprice:function() {

            var reslut = 0
            for(var i=0;i<this.goodList.length;i++){
                reslut = reslut + this.goodList[i].subtotal

            }
            return reslut
        }   
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
*{
    margin: 0;padding:0;
}
table {
    width: 980px;
    background: blue+220;
    margin: 0 auto;
    border-collapse: collapse;
    thead {
        background: blue+111;
        padding:8px;
        border:1px solid red;
        tr {
              height: 30px;

        }
      
    }
    .goods span {
        float: left;
        margin-top: 46px;
    }
    .goods img {
        width: 100px;
        height: 100px;
        background:pink;
        vertical-align: middle;
        margin-left:50px;
        margin-right: 20px;
        margin-top: 5px;
        margin-bottom: 5px;
        float: left;
        box-sizing: border-box;

    }
    .goods-number input{
        width: 60px;
        text-align: center;
    }
    .goods-number span {
        cursor: pointer;
    }
}
.foot {
    width: 980px;
    margin: 0 auto;
    background: pink;
    height: 60px;
    line-height: 60px;
    .fl {
        float: left;
    }
    .fr {
        float: right;
    }
    .closing {
        background: grey;
        height: 60px;
        width: 60px;
        line-height:60px;
    }
    .selected {
        margin-right: 8px;
    }
}
</style>
