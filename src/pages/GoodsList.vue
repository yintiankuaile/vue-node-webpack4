<template>
  <!--//template标签里面需要有个根元素-->
    <div>
      <nav-header></nav-header>
      <nav-bread>
        <span>Goods</span>
      </nav-bread>
      <div class="accessory-result-page accessory-page">
        <div class="container">
          <div class="filter-nav">
            <span class="sortby">Sort by:</span>
            <a href="javascript:void(0)" class="default cur">Default</a>
            <a href="javascript:void(0)" class="price">Price <svg class="icon icon-arrow-short"><use xlink:href="#icon-arrow-short"></use></svg></a>
            <a href="javascript:void(0)" class="filterby stopPop" @click="showFilterPop">Filter by</a>
          </div>
          <div class="accessory-result">
            <!-- filter -->
            <div class="filter stopPop" id="filter" v-bind:class="{'filterby-show': filterBy}">
              <dl class="filter-price">
                <dt>Price:</dt>
                <dd><a href="javascript:void(0)" v-bind:class="{'cur': priceChecked == 'all'}" @click="setPriceFilter('all')">All</a></dd>
                <dd v-for="(price,index) in priceFilter">
                  <a href="javascript:void(0)" v-bind:class="{'cur':priceChecked == index}" @click="setPriceFilter(index)">{{price.startPrice}} - {{price.endPrice}}</a>
                </dd>
              </dl>
            </div>

            <!-- search result accessories list -->
            <div class="accessory-list-wrap">
              <div class="accessory-list col-4">
                <ul>
                  <li v-for="(item,index) in goodList">
                    <div class="pic">
                      <!--<a href="#"><img v-bind:src="'/static/'+item.productImg" alt=""></a>-->
                      <a href="#"><img v-lazy="'/static/'+(index + 1)+'.jpg'" alt=""></a>
                    </div>
                    <div class="main">
                      <div class="name">{{item.productName}}</div>
                      <div class="price">{{item.productPrice}}</div>
                      <div class="btn-area">
                        <a href="javascript:;" class="btn btn--m">加入购物车</a>
                      </div>
                    </div>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="md-overlay" v-show="overLayFlag" @click="closePop"></div>
      <nav-footer></nav-footer>
    </div>
</template>

<script>
  import '../assets/css/base.css'
  import '../assets/css/product.css'
  import '../assets/css/login.css'
  import NavHeader from '@/components/NavHeader'
  import NavFooter from '@/components/NavFooter'
  import NavBread from '@/components/NavBread'
    export default {
        name: "GoodsList",
      data(){
        return {
          goodList: [],
          //价格列表
          priceFilter: [
            {
              startPrice: '0.00',
              endPrice: '500.00'
            },
            {
              startPrice: '500.00',
              endPrice: '1000.00'
            },
            {
              startPrice: '1000.00',
              endPrice: '2000.00'
            },
            {
              startPrice: '2000.00',
              endPrice: '3000.00'
            }
          ],
          // 价格筛选按钮高亮控制
          priceChecked: 'all',
          //响应式布局点击按钮后价格筛选按钮显示隐藏控制
          filterBy: false,
          //点击按钮后遮罩层出现控制
          overLayFlag: false
        }
      },
      components:{
        NavHeader,
        NavFooter,
        NavBread
      },
      mounted () {
        this.getGoodsList();
      },
      methods: {
          getGoodsList (){
            this.$axios.get("http://rap2api.taobao.org/app/mock/125352/goodslist").then((res) => {
              let db = res.data;
              this.goodList = db.result;
              console.log(db.result)
            })
          },
        showFilterPop (){
          this.filterBy = true;
          this.overLayFlag = true;
        },
        setPriceFilter (index){
            this.priceChecked = index;
            this.closePop();
        },
        closePop (){
            this.filterBy = false;
            this.overLayFlag = false;
        }
      }
    }
</script>

