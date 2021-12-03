<template>
  <div class="testingcomputedandmethods">
      <p>{{Number1}}</p>
      <p>{{Number2}}</p>
      <h2> {{ total }} </h2>
      <p>{{sum}}</p>
      <button @click="ontotal()">clickTOTAL</button>
      <button @click="clickNumber1Plus()">plusNum1</button>
  </div>
  <teleport to='body' >
    <modal-base v-if="isShowModal" title="Orange JUICE" content="Price : 20000" theme="sales" @closeModal="ShowModal"/>
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
    }
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
</style>
