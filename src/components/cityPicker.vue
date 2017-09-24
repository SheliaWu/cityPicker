<template>
  <div>
    <select class="province">
      <option v-for=""><option>
    </select>
    <select class="city">
      <option v-for=""><option>
    </select>
    <select class="dist">
      <option v-for=""><option>
    </select>
  </div>
</template>

<script>
  export default{
    name: 'cityPicker',
    data () {
      return{
        citys:null
      }
    },
    mounted() {
      this.getData()
    },
    methods: {
      getData:function() {
        this.$http.get('../../static/city-data.json')
          .then((response) => {
            this.citys = response.body
            console.log(this.citys)
          }, response => {
            console.log("error")
          })
      }
    }
  }
</script>