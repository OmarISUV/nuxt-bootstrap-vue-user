<template>
    <div>
        <b-table striped hover :items="items"></b-table>
        <b-button :on-click="getUser()" variant="info" size="sm">Actualizar Datos</b-button>
    </div>
</template>
  
<script>
export default {

    data() {
        return {
            items: []
        }
    },
    methods: {
        async getUser() {
            let res = await this.$axios.get('/api/user')
            this.items = res.data
        }
    },
    mounted() {
        this.getUser()
    },


}
</script>