<template>
<modal name="demo-login" transition="pop-out" :width="modalWidth" :focus-trap="true" :height="600">
  <div class="box ">
    
      <div class="text-center mt-5">
        <h3>REGISTRO DEL PACIENTE</h3>
      </div>
      <form
        @submit.prevent="registrarPaciente({correo: $v.paciente.correo.$model, contrasena:$v.paciente.contrasena.$model},
        {nombre: $v.pacienteDatos.nombre.$model,
        apellido: $v.pacienteDatos.apellido.$model,
        dni: $v.pacienteDatos.dni.$model,
        edad: $v.pacienteDatos.edad.$model,
        genero: $v.pacienteDatos.genero.$model,
        discapacidad:$v.pacienteDatos.discapacidad.$model,
        telefono: $v.pacienteDatos.telefono.$model,
        direccion: $v.pacienteDatos.direccion.$model})"
      >
      
       <div class="my-2 ml-5 mr-5" style="padding: 0px 12px 0px 10px; background-color: white;">
         <hr>
           <div class="form-row">
            <div class="form-group col-md-6 mt-4">
              <input type="text" class="form-control" placeholder="Usuario" id="inputUsuario" />
            </div>
            <div class="form-group col-md-6 mt-4">
              <input
                type="email"
                class="form-control"
                id="inputEmail4"
                v-model="$v.paciente.correo.$model"
                placeholder="Correo"
              />
            </div>
          </div>
          <div class="form-row ">
                <div class="form-group col-md-6 ">
                <input
                    type="password"
                    class="form-control"
                    id="inputPassword4"
                    v-model="$v.paciente.contrasena.$model"
                    placeholder="Contraseña"
                />
                </div>
                <div class="form-group col-md-6" >
                <input 
                    type="password" 
                    class="form-control" 
                    id="inputNewPassword4" 
                    placeholder="Repita Contraseña"
                />
                </div>
          </div>
          <div class="form-row">
            <div class="form-group col-md-6">
              <input
                type="text"
                class="form-control"
                id="inputName"
                v-model="$v.pacienteDatos.nombre.$model"
                placeholder="Nombres"
              />
            </div>
            <div class="form-group col-md-6">
              <input
                type="text"
                class="form-control"
                id="inputLastName"
                v-model="$v.pacienteDatos.apellido.$model"
                placeholder="Apellidos"
              />
            </div>
          </div>
          <div class="form-row">
            <div class="form-group col-md-6">
              <input
                type="text"
                class="form-control"
                id="inputDni"
                v-model="$v.pacienteDatos.dni.$model"
                placeholder="DNI"
              />
            </div>
            <div class="form-group col-md-6">
              <select id="inputState" class="form-control" 
              v-model="$v.pacienteDatos.genero.$model">
                <option selected>-- Sexo --</option>
                <option value="femenino">Femenino</option>
                <option value="masculino">Masculino</option>
              </select>
            </div>
        </div>
        <div class="form-row">
            <div class="form-group col-md-6">
              <input
                type="number"
                class="form-control"
                id="inputEdad"
                v-model="$v.pacienteDatos.edad.$model"
                placeholder="Edad"
              />
            </div>
            <div class="form-group col-md-6">
              <input
                type="text"
                class="form-control"
                id="inputDiscapacidad"
                v-model="$v.pacienteDatos.discapacidad.$model"
                placeholder="Discapacidad"
              />
            </div>
          </div>
          <div class="form-row">
            <div class="form-group col-md-6">
              <input
                type="number"
                class="form-control"
                id="inputCelular"
                v-model="$v.pacienteDatos.telefono.$model"
                placeholder="Número de Celular"
              />
            </div>
            <div class="form-group col-md-6">
              <input
                type="text"
                class="form-control"
                id="inputDireccion"
                placeholder="Dirección 'Calle siempre viva...'"
                v-model="$v.pacienteDatos.direccion.$model"
              />
            </div>
          </div>
           <br />
           <div class="alert alert-danger" role="alert" v-if="carga!=true">
            <div class="label">{{mensaje}}</div>
           </div>
           <hr>
          <div class="row justify-content-center">
          <div class="col-12 col-sm-10 col-xl-6 text-center">
            <input
              type="submit"
              class="butn"
              value="REGISTRAR"
              :disabled="$v.$invalid || carga2"
            />
          </div>
       </div>
       
        </div>
        <br />
        
      </form>
    </div>

</modal>
</template>
<script>
import { required, minLength, email } from "vuelidate/lib/validators";
const MODAL_WIDTH = 800

export default {
  name: 'DemoLoginModal',
  data() {
    return {
      mensaje: "",
      modalWidth: MODAL_WIDTH,
      paciente: {
        correo: "",
        contrasena: ""
      },
      pacienteDatos: {
        nombre: "",
        apellido: "",
        edad: "",
        genero: "",
        direccion: "",
        telefono: "",
        dni: "",
        discapacidad: ""
      },
      mensaje: null,
      carga: true,
      carga2: null
    }
  },
  created() {
    this.modalWidth =
      window.innerWidth < MODAL_WIDTH ? MODAL_WIDTH / 2 : MODAL_WIDTH
  },
  validations: {
    paciente: {
      correo: {
        required,
        email
      },
      contrasena: {
        required,
        minLength: minLength(4)
      }
    },
    pacienteDatos: {
      nombre: { required },
      apellido: { required },
      edad: { required },
      genero: {required},
      direccion: { required },
      telefono: { required },
      dni: { required },
      discapacidad: { required }
    }
  },
  methods: {
    registrarPaciente(paciente, pacienteDatos) {
      this.carga2=true;
      this.paciente = paciente;
      this.pacienteDatos = pacienteDatos;
      this.axios
        .post("https://proyectocalidad9.herokuapp.com/paciente/registro", {
        //.post("http://localhost:1400/paciente/registro", {
          ...this.paciente,
          ...this.pacienteDatos
         
        })

        .then(res => {
          this.carga = true;
          this.$modal.hide('demo-login')
          this.carga2=false;
          
        })
        .catch(e => {
          this.mensaje = e.response.data.message;
          this.carga = false;
          this.carga2=false;
        });
    }
  }
};
</script>
<style lang="scss" scoped>
$background_color: #404142;
$github_color: #dba226;
$facebook_color: #3880ff;

.box {
  background: white;
  overflow: hidden;
  width: 800px;
  height: 600px;
  border-radius: 2px;
  box-sizing: border-box;
  box-shadow: 0 0 40px black;
  color: #025f8ace;
  font-size: 0;

  

  .box-messages {
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
  }

  .box-error-message {
    position: relative;
    overflow: hidden;
    box-sizing: border-box;

    height: 0;
    line-height: 32px;
    padding: 0 12px;
    text-align: center;
    width: 100%;
    font-size: 11px;
    color: white;
    background: #f38181;
  }
  .label {
    width: 100%;
    height: 100%;
    font-size: 13px;
    color:  #494949;
    font-weight: bold;
  }
.butn {
    background-color: transparent;
    text-transform: uppercase;
    border: 1px solid #025f8ace ;
    padding: 10px 20px;
    margin: 5px 0px;
    color: #025f8ace ;
    font-size: 14px;
    letter-spacing: 1px;
    opacity: 0.7;
    font-weight: bold;
}
.butn:hover {
    opacity: 1;
    background-color: #03a8f4d5 ;
    color: white; 
}
  


  button {
    background: white;
    border-radius: 4px;
    box-sizing: border-box;
    padding: 10px;
    letter-spacing: 1px;
    font-family: 'Open Sans', sans-serif;
    font-weight: 400;
    min-width: 140px;
    margin-top: 8px;
    color: #8b8c8d;
    cursor: pointer;
    border: 1px solid #dddedf;
    text-transform: uppercase;
    transition: 0.1s all;
    font-size: 10px;
    &:hover {
      border-color: mix(#dddedf, black, 90%);
      color: mix(#8b8c8d, black, 80%);
    }
  }

  .large-btn {
    width: 100%;
    background: white;

    span {
      font-weight: 600;
    }
    &:hover {
      color: white !important;
    }
  }

  .button-set {
    margin-bottom: 8px;
  }

  #register-btn,
  #signin-btn {
    margin-left: 8px;
  }

  .facebook-btn {
    border-color: $facebook_color;
    color: $facebook_color;
    &:hover {
      border-color: $facebook_color;
      background: $facebook_color;
    }
  }

  .github-btn {
    border-color: $github_color;
    color: $github_color;
    &:hover {
      border-color: $github_color;
      background: $github_color;
    }
  }

  .autocomplete-fix {
    position: absolute;
    visibility: hidden;
    overflow: hidden;
    opacity: 0;
    width: 0;
    height: 0;
    left: 0;
    top: 0;
  }
}

.pop-out-enter-active,
.pop-out-leave-active {
  transition: all 0.5s;
}

.pop-out-enter,
.pop-out-leave-active {
  opacity: 0;
  transform: translateY(24px);
}
</style>
