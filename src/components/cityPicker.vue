<template>
  <div>
    <select class="province" @change="selectProv">
      <option :value="index" v-for="(item,index) in provinces">{{item}}</option>
    </select>
    <select class="city" @change="selectCity">
      <option :value="index" v-for="(item,index) in citys">{{item}}</option>
    </select>
    <select class="dist" @change="selectDist">
      <option :value="index" v-for="(item,index) in dists">{{item}}</option>
    </select>
  </div>
</template>

<script>
  export default{
    name: 'cityPicker',
    data () {
      return{
        dtaArr:null,
        provinces:[],
        citys:[],
        dists:[],
        select:[]
      }
    },
    mounted() {
      this.getData()
    },
    methods: {
      getData:function() {
        this.$http.get('../../static/city-data.json')
          .then((response) => {
            this.dataArr = response.body
            console.log(this.dataArr)
            this.dataArr.forEach((item) => {
              this.provinces.push(item.name)
            })
            this.select = this.dataArr[0]
            let province = this.select.children
            province.forEach((item) => {
              this.citys.push(item.name)
            })
            let dist = this.select.children[0].children
            dist.forEach((item) => {
              this.dists.push(item.name)
            })

          }, response => {
            console.log("error")
          })
      },
      selectProv: function(ele) {
        let index = ele.target.value
        //清除数据
        this.citys = []
        this.dists = []
        this.select = this.dataArr[index]
        let province = this.select.children
        province.forEach((item) => {
          this.citys.push(item.name)
        })
        let dist = this.select.children[0].children
          dist.forEach((item) => {
            this.dists.push(item.name)
          })
      },
      selectCity: function(ele) {
        let index = ele.target.value
        this.dists = []
        let dist = this.select.children[index].children
          dist.forEach((item) => {
            this.dists.push(item.name)
          })
      },
      selectDist: function() {

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
</style>