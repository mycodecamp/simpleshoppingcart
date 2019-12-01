<template>
  <div class="shopit">
 
      
    <Header :cartcounter="countCart" :shoppingcart="cartList" :totalprice="totalPrice"  @remove-Cart="removeItem" @checkCartOut="checkCartOut"/>

    <div class="laptoplist py-5 bg-light">
      <div class="container">           
        <div class="row">          
         
            <ProductList v-for="(laptop, index) in laptops" :key="laptop.id">
             
              <template v-slot:price>{{ laptop.price | currencyfilter}}</template>
              <template v-slot:name>{{ laptop.name }}</template>
              
              <template v-slot:image><img :src="laptop.image" width="100%" height="225" :alt="laptop.name"></template>
              
              <template v-slot:laptopcolors>
                <b-form-radio-group id="btn-radios-1" v-model="laptopColorChecked[index]" :options="laptop.colors" buttons name="radios-btn-default" button-variant="outline-secondary" ></b-form-radio-group>
              </template>

              <template v-slot:addToCartBtnSlot>
                <button type="button" class="btn btn-sm btn-primary add-to-cart" id="CartBtn" @click="addtocart(laptop,index)">Add to cart</button>
              </template>
            </ProductList>

          
        </div>
      </div>
    </div>   
    
    <Footer/>

    <div class="Check-out-box" v-show="showcheckout">
      <div class="Check-out-wrapper">
        <div class="Check-out-container">
          <div class="checkoutclose"><a href="#" @click="closeCheckout"><font-awesome-icon icon="times" size="1.5x"/></a></div>

          <div class="Check-out-head">
            <h2>Check out</h2>
          </div>

          <div class="check-out-body">Thank you for shopping with us.</div>
          
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Header from "@/components/Header";
import ProductList from "@/components/ProductList";
import Footer from "@/components/Footer";


export default { 
  components: {
    Header,
    ProductList,
    Footer
  },  
  data () {
    return { 
      defaultColor: '0' , 
      cartList: [] ,     
      laptops: null ,
      laptopColorChecked: [],
      showcheckout: false
      
    }
  },
  created: function () {
    this.laptops = [
          {
            name: "Macbook",
            price: 899.99,
            image:"https://cdn.pixabay.com/photo/2014/05/02/21/47/workstation-336369_1280.jpg",
            colors:["White","Silver"]
          },
          {
            name: "Acer",
            price: 499.00,
            image:"https://cdn.pixabay.com/photo/2015/05/31/10/51/acer-791027_1280.jpg",
            colors:["Silver"]
          },
          {
           name: "Samsung",
            price: 899.99,
            image:"https://cdn.pixabay.com/photo/2014/07/30/22/53/notebook-405755_1280.jpg",
            colors:["Black"]
          },
          {
           name: "Microsoft Surface",
            price: 1290.90,
            image:"https://cdn.pixabay.com/photo/2018/09/07/05/41/surface-book-3660000_1280.jpg",
            colors:["Black", "Red", "Blue"]
          },
          {
           name: "Lenovo Thinkpad",
            price: 635.60,
            image:"https://cdn.pixabay.com/photo/2016/04/17/17/43/lenovo-thinkpad-x61-tablet-1335138_1280.jpg",
            colors:["Black","Silver"]
          },
          {
           name: "HP",
            price:579.90,
            image:"https://cdn.pixabay.com/photo/2016/06/08/10/35/laptop-1443559_1280.jpg",
            colors:["Teal","Navy"]
          },
          {
           name: "Asus",
            price: 428.90,
            image:"https://cdn.pixabay.com/photo/2014/09/27/13/45/notebook-463490_1280.jpg",
            colors:["Black", "Red"]
          },
          {
           name: "MSI",
            price: 345.00,
            image:"https://cdn.pixabay.com/photo/2012/04/13/20/24/laptop-33521_1280.png",
            colors:["Black"]
          },
          {
           name: "Dell",
            price: 289.90,
            image:"https://cdn.pixabay.com/photo/2017/01/06/00/45/computer-1956711_1280.png",
            colors:["Black", "Blue"]
          }
      ]
  },
  mounted: function () {
    this.laptopColorChecked=this.selectdefaultcolor(this.laptops)
   
  },  
  methods: {
    addtocart: function(laptop, index) {

        var mycart={
            name: laptop.name,
            price: laptop.price,
            image:laptop.image,
            color: this.laptopColorChecked[index]
        }

        this.cartList.push(mycart);
    }, 
    selectdefaultcolor  : function(laptops) {
      var mycolors=new Array();
      laptops.forEach(function(laptop){
        mycolors.push(laptop.colors[0]);          
      })

      return mycolors;
    },
    removeItem : function(cartind) {
       //this.cartList.remove(cartind);
       this.$delete(this.cartList, cartind)
    },
    checkCartOut : function(){
      this.cartList=[];
      this.showcheckout=true;
    },
    closeCheckout: function(){
      this.showcheckout=false;
    }
  },
  computed: {  
    countCart: function(){
      return this.cartList.length;
    },
    totalPrice: function(){
      var sumprice=0;
      var cartlistval=this.cartList;
      cartlistval.forEach(function(laptop){
          sumprice+=laptop.price;
      })
      return sumprice;
    }
  }
  
}
</script>


<style scoped>
.shopit{
    
}
.container {
  max-width: 960px;
}


.Check-out-box {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .5);
  display: table;
  transition: opacity .3s ease;
}

.Check-out-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.Check-out-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
  transition: all .3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.Check-out-head h2 {
  margin-top: 0;
  color:#ccc;
  border-bottom:2px solid #aaa;
}
.check-out-body {
  padding:10px;
  text-align:center;
}
.checkoutclose {
  text-align:right;
}
.checkoutclose  a {
  color:red;
  
}



</style>
