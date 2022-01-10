<template>
    <div>
        <h1>Iniciar sesión</h1>
        <form @submit.prevent="iniciarSesion">
            <input v-model="usuario" placeholder="Usuario" />
            <input v-model="contrasenia" placeholder="contrasenia"/>
            <input type="submit" value="Iniciar Sesión" />
        </form>
        +5+TRAK0Gkg1bgqmfUTjsnTdDyY37YWnPPRkg86mygjxoLc6uukg8ONm5ZwyrX9zZgi3nuVaj+KiaCsywWQ5+w==
        {{ mensajeError }}
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            usuario: '',
            contrasenia: '',
            mensajeError: ''
        }
    },
    methods: {
        iniciarSesion() {
            let req = {
                "Usuario": this.usuario,
                "Contrasenia": this.contrasenia
            };            
            axios.post('https://localhost:44382/api/Evaluador/validarCredenciales', req)
            .then(data => {
                if(data.status == 200) {
                    this.$router.push('/Siniestros')
                }
            }).catch(() =>{
                this.mensajeError = "Credenciales inválidas"
            })
        }
    }
}
</script>