<template>
    <div class="row">
        <div class="col-md-2"></div>
        <div class="col-md-8">
            <div class="card">
                <form @submit.prevent="sendForm()">
                    <div class="card-header text-center">{{ title }}</div>
                    <div class="card-body">
                        <div class="row">
                            <div class="col-md-12">
                                <input type="email" placeholder="Escriba su correo" class="form-control mb-2" :class="{'error':validarEmail}" v-model="form.correo" >
                            </div>
                        </div>
                        <div class="row" v-if="form.type!=2">
                            <div class="col-md-12">
                                <input type="password" placeholder="Contraseña" class="form-control mb-2" :class="{'error':validarPassword}" v-model="form.clave">
                            </div>
                        </div>
                        <div class="row" v-if="form.type==1">
                            <div class="col-md-12">
                                <input type="password" placeholder="Repetir contraseña" class="form-control mb-2" :class="{'error':validaRepetirPassword}" v-model="form.clave2">
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-sm-1"></div>
                            <div class="col-sm-4">
                                <input type="submit" class="btn btn-info" value="Iniciar Sessión" name="inicio">
                            </div>
                            <div class="col-sm-2"></div>
                            <div class="col-sm-4">
                                <input type="reset" class="btn btn-danger" value="Cancelar">
                            </div>
                            <div class="col-sm-1"></div>
                        </div>
                        <div class="row">
                            <div class="col-sm-2"></div>
                            <div class="col-sm-4" v-if="form.type!=2">
                                <a href="javascript:void(0)" @click="form.type=2">Recuperar contraseña</a>
                            </div>
                            <div class="col-sm-4" v-if="form.type!=1">
                                <a href="" @click="form.type=1">Registrarme</a>
                            </div>
                            <div class="col-sm-4" v-if="form.type!=0">
                                <a href="javascript:void(0)" @click="form.type=0" >Iniciar sesión</a>
                            </div>
                            <div class="col-sm-2"></div>
                        </div>
                    </div>
                </form>
            </div>
        </div>
        <div class="col-md-2"></div>
    </div>
</template>

<script>
    export default {
        name: "login",
        data() {
            return { form: {
                    type: 0, // 0 = Login , 1 = Registro 2- Recuperar contraseña
                    correo: "",
                    clave: "",
                    clave2: "",
                } }
        },
        methods: {
            sendForm: function(){
                if(this.validaType()){
                    console.log(this.form);
                }
            },
            validaType: function(){
                if(this.form.type==0 && !this.validarEmail() && !this.validarPassword()){
                    return true;
                }
                else if(this.form.type==1 && !this.validarEmail && !this.validaRepetirPassword){
                    return true;
                }
                else if(this.form.type==2 && !this.validarEmail){
                    return true;
                }
                return false;
            },
        },
        computed: {
            validarEmail: function(){
                var exp = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3,4})+$/;
                if(exp.test(this.form.correo)){
                    return false;
                }
                else {
                    return true;
                }
            },
            validarPassword: function () {
                var exp = /^(?=.*\d)(?=.*[a-záéíóúüñ]).*[A-ZÁÉÍÓÚÜÑ]/;
                if (exp.test(this.form.clave)){
                    return false;
                }
                else {
                    return true;
                }
            },
            validaRepetirPassword: function (){
                if(this.form.clave==this.form.clave2){
                    return false;
                } else{
                    return true;
                }
            },
            title: function (){
                return (this.form.type==0)?'Login':(this.form.type==1)?'Registro':'Recuperar contraseña';
            }
        }
    }
</script>

<style scoped>
    .error{
        border-bottom: 3px solid red;
    }
</style>
