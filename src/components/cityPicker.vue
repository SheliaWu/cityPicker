<template>
  <div>
  <div class="wrapper">
      <select class="province" @change="selectProv" v-model="index1">
        <option :value="index" v-for="(item,index) in provinces" v-bind:key="index" >{{item}}</option>
      </select>
      <select class="city" @change="selectCity"  v-model="index2">
        <option :value="index" v-for="(item,index) in citys" v-bind:key="index">{{item}}</option>
      </select>
      <select class="dist" @change="selectDist" v-model="index3">
        <option :value="index" v-for="(item,index) in dists" v-bind:key="index">{{item}}</option>
      </select>
  </div>
  <div class="show_result">选择的地点为：{{provinces[index1]}}-{{citys[index2]}}->{{dists[index3]}}</div>
  </div>
</template>

<script>
  import axios from  'axios'
  export default{
    name: 'cityPicker',
    data () {
      return{
        dtaArr:null,
        provinces:[],
        citys:[],
        dists:[],
        index1:0,
        index2:0,
        index3:0
      }
    },
    created() {
      this.initialData()
    },
    methods: {
      initialData:function() {
        axios.get('./static/city-data.json')
          .then((res) => {
            this.dataArr = res.data
            this.dataArr.forEach((item) => {
              this.provinces.push(item.name)
            })
            let initialProv = this.dataArr[0]
            this.province = this.dataArr[0].name
            let citys = initialProv.children
            this.city = this.dataArr[0].children[0].name
            citys.forEach((item) => {
              this.citys.push(item.name)
            })
            let dists = initialProv.children[0].children
            this.city = this.dataArr[0].children[0].children[0].name
            dists.forEach((item) => {
              this.dists.push(item.name)
            })
          })
          .catch(err => console.log(err))
      },
      selectProv: function(ele) {
        this.index1 = ele.target.value
        this.index2 =  0
        this.index3 = 0
        this.renderCitys()
        this.renderDists()
      },
      selectCity: function(ele) {
        this.index2 = ele.target.value
        this.index3 = 0
        this.renderDists()
      },
      selectDist: function(ele){
        this.index3 = ele.target.value
      },
      renderCitys(){
        this.citys = []
        let citys = this.dataArr[this.index1].children
        citys.forEach((item) => {
          this.citys.push(item.name)
        })
      },
      renderDists(){
        this.dists = []
        let dists = this.dataArr[this.index1].children[this.index2].children
        dists.forEach((item) => {
          this.dists.push(item.name)
        })
      }
    }
  }
</script>
<style scoped>
  select{
    margin:2px 2px;
    width:80px;
    height:25px;
  }
  select:focus{
    outline:none;
  }
  .show_result{
    margin-top: 20px;
    text-align:center;
  }
</style>