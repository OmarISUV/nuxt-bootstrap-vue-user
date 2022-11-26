<template>
    <div>
        <b-form @submit="onSubmit" @reset="onReset" v-if="show">
            <b-form-group id="input-group-2" label="Nombre Completo:" label-for="input-2">
                <b-form-input id="input-2" v-model="form.name" placeholder="Ingresa tu Nombre" required></b-form-input>
            </b-form-group>
            <b-form-group id="input-group-1" label="Email:" label-for="input-1">
                <b-form-input id="input-1" v-model="form.email" type="email" placeholder="Ingresa tu email" required>
                </b-form-input>
            </b-form-group>
            <b-button type="submit" variant="primary">Registrar</b-button>
            <b-button type="reset" variant="danger">Limpiar</b-button>
        </b-form>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            form: {
                email: '',
                name: '',
            },
            items: [],
            show: true
        }
    },
    methods: {
        async onSubmit(event) {
            event.preventDefault()
            let res = await this.$axios.post('/api/user',
                {
                    name: this.form.name,
                    email: this.form.email
                })
            console.log(res)
            if (res) {
                alert("User", res.statusText)
            }
        },
        onReset(event) {
            event.preventDefault()
            // Reset our form values
            this.form.email = ''
            this.form.name = ''
            // Trick to reset/clear native browser form validation state
            this.show = false
            this.$nextTick(() => {
                this.show = true
            })
        }
    }
}
</script>