<template>


 <div id="app">
  <button v-on:click="$destroy()">Destroy instance</button>
  <div id="change-array-index" v-cloak="v-cloak">
  <input type="text" v-model="animal" />
  <button :disabled='isDisabled' v-on:click="changeAnimal">Change Animal</button>
  <ul>
    <li v-for="item in animals" v-bind:key="item">{{ item }}</li>
  </ul>
  <keep-alive> 
  <button v-if='!isDisabled' v-on:click.once="$forceUpdate()">forceUpdate</button>
  </keep-alive>
  <button v-show='!isDisabled' v-on:click="$forceUpdate()">forceUpdate</button>

</div>
    <div>Computed: {{dateComputed}}</div>
    <div>Method: {{dateMethod()}}</div>
    <div>Watch: {{dateWatch}}</div>
  <p>123 {{message}}</p>
  <p v-text="message">123 {{message}}</p><!--interpolation & v-text  -->
  <button @click="addCount('dog')">addDogs</button>
  <button @click="addCount('cat')">addCats</button>
  <button @click="addCount('penguin')">addPenguin</button>
  <p>dog {{ counter.dog }}, cat {{ counter.cat }}, penguin {{ counter.penguin }}</p>
  <button @click="$destroy()">Destroy instance</button>
  <select v-model="myName">
    <option v-for="(item, index) in member" :key="index">{{ item }}{{index}}</option>
  </select>
  <p>Name：{{ myName }}</p>
  <li v-for="(i, k) of object">
    {{ i }}{{k}}
  </li>
  <component>
    <card/>
  </component>
</div>

</template>

<script>
  import card from './components/card';
  var counter = {
    dog: 0,
    cat: 0}

    Object.freeze(counter) 

    
    export default {
      name: 'app',
      components: {
    card,
  },
      data() {
        return {
          message:"eoijgihg",
          animal: "init",
          animals: ['<Animal>', 'cat', 'penguin', 'bird', 'rabbit'],
          myName:'myName',
          member:['Adam','Jack','Candy','Louis','Lurry'],
          object: {
            title: 'How to do lists in Vue',
            author: 'Jane Doe',
            publishedAt: '2016-04-10'
          }, 
          counter:{
            dog: 0,
            cat: 0},
            isDisabled : false
          }
      },
      watch:{
        dateWatch() {
            return Date.now();
          }
        },
       computed:{
        dateComputed() {
            return Date.now();
          }

        },
      methods: {
        dateMethod() {
      return Date.now();
    },
        addCount(name) {
          this.counter[name] ++
        },
        changeAnimal(){
            // 利用 arr.splice(startIndex, deleteCount, addItem)
            this.animals.splice(0, 1, this.animal)
            // 利用陣列索引直接設置值
            // this.animals[0] = this.animal
            // 利用 vm.$set(array, index, value) 方法
            // this.$set(this.animals, 0, this.animal)
          }
        },
        beforeCreate() {
          console.log('beforeCreate');
          console.log(` this.message: ${this.message}`);
          console.log(` this.el: ${this.$el}`);
        },
        created() {
          console.log('created');
          console.log(` this.message: ${this.message}`);
          console.log(` this.el: ${this.$el}`);
          console.log(this);
        },
        beforeMount() {
          console.log('beforeMount');
          console.log(this.$el.outerHTML);
          console.log();
        },
        mounted(){  
          console.log('mounted');
          console.log(this.$el.outerHTML);
          console.log();

    //透過建立新的物件來新增物件的屬性   
    // this.counter = Object.assign({}, this.counter, { penguin: 0 })
    // 動態新增響應式的屬性
    // this.$set(this.counter, 'penguin', 0)
    // 在 created 的時候才建立 penguine 順便設值為 0
    this.counter.penguin = 0
        },
        beforeUpdate(){

         console.log('beforeUpdate');
         console.log(` this.counter: ${this.counter.dog}`);
         console.log(` this.$el: ${this.$el}`);
         console.log(this.$el.outerHTML);
         console.log();
        },
        updated() {
          // 讓我們可以知道組件有被更新
          console.log('updated');
          console.log(` this.counter: ${this.counter.dog}`);
          console.log(` this.$el: ${this.$el}`);
          console.log(this.$el.outerHTML);
          console.log();
        },
        activated(){
          console.log('activated');

        },
        deactivated(){
          console.log('deactivated');

        },
        beforeDestroy() {
          console.log('beforeDestroy');
          console.log();
        },
        destroyed() {
          console.log('destroyed');
          console.log();
        },

       
      }
    </script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
