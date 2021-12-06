<template v-cloak>
  <!-- OptionApo - Directives -->
  <div v-html="title"></div>
  <span v-text="content"></span>
  <br>
  <!-- v-show chỉ là display - none hoặc block chứ k mất đi -->
  <div v-show="isShow">This is my homepage</div>
  <button @click="isShow = !isShow">Show HomePage</button>
  <!-- v-if v-else v-else-if  -->

  <div v-if="testing == 1">Show Products</div>
  <div v-else-if="testing==2">Products updated</div>
  <div v-else>Products deleted</div>
  <button @click="TestingIfElse(1)">Show</button>
  <button @click="TestingIfElse(2)">Update</button>
  <button @click="TestingIfElse(3)">Delete</button>
  <br>
  <!-- v-for  -->
  <button @click="ShowProduct = !ShowProduct">Show Menu</button>
  <div class="blocklistproduct">
    <div v-show="ShowProduct" v-for="product in products" :key="product.Id" style="padding:20px;cursor:pointer">
        <div>
          {{ product.Id }}
        </div>
        <img :src="product.Image"  style="height:100px;width:100px"/>
        <div>
          {{product.Name}}
        </div>
        <div>
          {{product.Price}}
        </div>
    </div>
  </div>
  <!-- v-model -->
  
    <input type="text" v-model="testingvmodel">
    <div>{{testingvmodel}}</div>
  <!-- v-once -->
  <div v-once>
    <h2>{{once}}</h2>
  </div>
  <div>
    <h2>{{changeonce()}}</h2>
  </div>

  <!-- OptionApi - Data -->
  <div class="testingcomputedandmethods">
      <p>{{Number1}}</p>
      <p>{{Number2}}</p>
      <h2> {{ total }} </h2>
      <p>{{sum}}</p>
      <button @click="ontotal()">clickTOTAL</button>
      <button @click="clickNumber1Plus()">plusNum1</button>
  </div>
  <!-- v-slot -->
  <teleport to='body' >
    <modal-base v-if="isShowModal" @closeModal="ShowModal"> 
      <template v-slot:header>
        <h2>Header</h2>
      </template>
      <div>
        <h2>Body</h2>
      </div>
      <template v-slot:footer>
        <h2>Footer</h2>
      </template>
    </modal-base>
  </teleport>
    <button @click="ShowModal">Click to Show Modal</button>
</template>

<script>
import ModalBase from './components/ModalBase.vue';

export default {
  components: { ModalBase },
  name: "App",
  component:{
    ModalBase,
  },
  expose: ['ontotal'],
  data() {
    return {
      isShowModal:false,
      Number1:1,
      Number2:2,
      sum:0,
      title:'<h1 style="color:red">Coffee House</h1>',
      content:'Mỗi lần về lại chốn cũ, nơi mà con người khác đi nhưng vị của tách cà phê đen vẫn không thay đổi.',
      isShow:false,
      testing:0,
      products: [
        {
          Id:1,
          Image:'https://quangtanhoa.com/wp-content/uploads/2018/01/ca-phe-den-da.jpg',
          Name:'Coffee Đen',
          Price:12000
        },
        {
          Id:2,
          Image:'https://dinhthaocoffee.com/wp-content/uploads/2018/07/ca_phe_sua_da.jpg',
          Name:'Coffee Sữa',
          Price:14000
        },
        {
          Id:3,
          Image:'https://classiccoffee.com.vn/files/common/ca-phe-chanh-mat-lanh-cho-ngay-he-nong-buc-ymne8.jpg',
          Name:'Coffee Chanh',
          Price:18000
        }
      ],
      ShowProduct:false,
      testingvmodel:'',
      once:'Hồ Xuân Tuấn Hùng',
    }
  },
  computed:{
    total(){
      return this.Number1+this.Number2; 
    }
  },
  methods: {
    ontotal(){
      this.sum=this.Number1+this.Number2;
    },
    clickNumber1Plus(){
      this.Number1++;
    },
    ShowModal(){
      this.isShowModal = !this.isShowModal;
    },
    TestingIfElse(number){
      this.testing=number;
    },
    changeonce(){
      this.once='Hùng';
      return this.once;
    },
  },
  watch:{
     Number1(val, oldVal) {
      console.log(`new: ${val}, old: ${oldVal}`)
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.testingcomputedandmethods{
  margin-bottom: 50px;
}
.blocklistproduct{
  display: flex;
  justify-content: center;
  align-items: center;
}
[v-cloak]{
  display: none;
}
</style>
