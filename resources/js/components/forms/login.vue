<template>
  <div>
    <b-table striped hover :items="items" :fields="fields"></b-table>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        items: null,
        fields: ['id', 'USERNAME']
      }
    },
    methods:{
      get_accounts(){
        axios.get('/get_accounts').then(response=>{
          console.log(response.data);
          this.items = response.data;
        }).catch(error=>{
          console.log(error.data);
        })
      }
    },

    methods: {
      register(){
        axios.post('/register/registration', this.form).then(response=>{
          console.log(response.data.email);
          console.log(response.data.password);
        }).catch(error=>{
          console.log(error.data);
          this.loading=false;
        })
      }
    },

    beforeMount(){
      this.get_accounts();
    }
  }
</script>