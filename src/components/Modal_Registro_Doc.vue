<template>
<modal name="demo-registro-doc" transition="pop-out" :width="modalWidth" :focus-trap="true" :height="600">
  <div class="box ">
      
    <!-- area de Formulario de Medico -->
    <div >
        
      <div class="text-center mt-2">
        <h2 >REGISTRO DEL MÉDICO</h2>
        <hr>
      </div>
      <form
        class="p-3 form"
        @submit.prevent="registrarDoctor({correo: $v.doctor.correo.$model, contrasena:$v.doctor.contrasena.$model},
        {nombre: $v.doctorDatos.nombre.$model, apellido: $v.doctorDatos.apellido.$model,
        dni: $v.doctorDatos.dni.$model,
        genero: $v.doctorDatos.genero.$model,
         edad: $v.doctorDatos.edad.$model, telefono: $v.doctorDatos.telefono.$model},
         {cmp: $v.doctorProfesion.cmp.$model, profesion: $v.doctorProfesion.profesion.$model,
         especialidad: $v.doctorProfesion.especialidad.$model, num_colegiatura: $v.doctorProfesion.num_colegiatura.$model,
         reg_especialidad: $v.doctorProfesion.reg_especialidad.$model})"
      >
     <div class="form-row">

     <div class="form-group col-md-6">
        <div class=" text-center">
          <h5 style="color: #025f8ace;">DATOS PERSONALES</h5>
        </div>
        <div class="mr-2" >
          <div class="form-row">
            <div class="form-group col-md-6 mt-4">
              <input type="text" class="form-control" id="inputUsuario" 
              placeholder="Usuario"/>
            </div>
            <div class="form-group col-md-6 mt-4">
              <input
                type="email"
                class="form-control"
                id="inputEmail4"
                v-model="$v.doctor.correo.$model"
                placeholder="Correo"
              />
            </div>
          </div>
          <div class="form-row">
            <div class="form-group col-md-6">
              <input
                type="password"
                class="form-control"
                id="inputPassword4"
                v-model="$v.doctor.contrasena.$model"
                placeholder="Contraseña"
              />
            </div>
            <div class="form-group col-md-6">
              <input type="password" class="form-control" id="inputNewPassword4" 
              placeholder="Repita Contraseña"/>
            </div>
          </div>
          <div class="form-row">
            <div class="form-group col-md-6">
              <input
                type="text"
                class="form-control"
                id="inputName"
                v-model="$v.doctorDatos.nombre.$model"
                placeholder="Nombres"
              />
            </div>
            <div class="form-group col-md-6">
              <input
                type="text"
                class="form-control"
                id="inputLastName"
                v-model="$v.doctorDatos.apellido.$model"
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
                v-model="$v.doctorDatos.dni.$model"
                placeholder="DNI"
              />
            </div>
            <div class="form-group col-md-6">
              <select id="inputState" class="form-control"
              v-model="$v.doctorDatos.genero.$model">
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
                v-model="$v.doctorDatos.edad.$model"
                placeholder="Edad"
              />
            </div>
            <div class="form-group col-md-6">
              <input
                type="number"
                class="form-control"
                id="inputtelefono"
                v-model="$v.doctorDatos.telefono.$model"
                placeholder="Número Telefónico"
              />
            </div>
          </div>
        </div>
     </div>

     <div class="form-group col-md-6 " style="border-left: 2px solid #c6c6c6;
        height: 340px; ">
        <div class=" text-center">
          <h5 style="color: #025f8ace;">DATOS PROFESIONALES</h5>
          
        </div>
        <div class="ml-2">
          <div class="form-row">
            <div class="form-group col-md-6 mt-4">
              <input
                type="text"
                class="form-control"
                id="inputCmp"
                v-model="$v.doctorProfesion.cmp.$model"
                placeholder="CMP"
              />
              
            </div>
            <div class="form-group col-md-6 mt-4">
              <input
                type="text"
                class="form-control"
                id="inputProfesion"
                v-model="$v.doctorProfesion.profesion.$model"
                placeholder="Profesión"
              />
            </div>
          </div>
          <div class="form-group">
            <input
              class="form-control"
              id="inputEspecialidad"
              v-model="$v.doctorProfesion.especialidad.$model"
              placeholder="Especialidad"
            />
          </div>
          <div class="form-row">
            <div class="form-group col-md-6">
              <input
                type="text"
                class="form-control"
                id="inputNumColeg"
                v-model="$v.doctorProfesion.num_colegiatura.$model"
                placeholder="Colegiatura"
              />
            </div>
            <div class="form-group col-md-6">
              <input
                type="text"
                class="form-control"
                id="inputRegEsp"
                v-model="$v.doctorProfesion.reg_especialidad.$model"
                placeholder="Registro especialidad"
              />
            </div>
          </div>
          <div class="label" style="font-weight: bold;">
              Muy Importante:
          </div>
          <div class="label">
              <dir>
                  -	Al ingresar la información se debe considerar la originalidad de la misma.
              </dir>
              <dir>
                  -	Además, considerar que los datos son confidenciales.
              </dir>
          </div>
        </div>
        <br />
        <small class="text-danger" style="font-weight: bold;" v-if="$v.mensaje != ''">{{mensaje}}</small>
     </div>
     </div>
     <div class="alert alert-danger" role="alert" v-if="carga!=true">
            <div class="label">{{mensaje}}</div>
      </div>
    <br>
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
      </form>
    </div>
     
    <!--ends -->
    
  </div>
    
</modal>
</template>
<script>
import vueCustomScrollbar from 'vue-custom-scrollbar'
import { required, minLength, email } from "vuelidate/lib/validators";
const MODAL_WIDTH = 800

export default {
  name: 'Modal_Registro_Doc',
  components: {
    vueCustomScrollbar
  },
  data() {
    return {
       settings: {
        maxScrollbarLength: 10
      },
      modalWidth: MODAL_WIDTH,
      doctor: {
        correo: "",
        contrasena: ""
      },
      doctorDatos: {
        nombre: "",
        apellido: "",
        dni: "",
        genero: "",
        edad: "",
        telefono: ""
      },
      doctorProfesion: {
        cmp: "",
        profesion: "",
        especialidad: "",
        num_colegiatura: "",
        reg_especialidad: ""
      },
      mensaje: null,
      carga: true,
      carga2:null
    };
  },
  created() {
    this.modalWidth =
      window.innerWidth < MODAL_WIDTH ? MODAL_WIDTH / 2 : MODAL_WIDTH
  },
  validations: {
    doctor: {
      correo: {
        required,
        email
      },
      contrasena: {
        required,
        minLength: minLength(4)
      }
    },
    doctorDatos: {
      nombre: { required },
      apellido: { required },
      dni: { required },
      genero: {required},
      edad: { required },
      telefono: { required }
    },
    doctorProfesion: {
      cmp: { required },
      profesion: { required },
      especialidad: { required },
      num_colegiatura: { required },
      reg_especialidad: { required }
    }
  },

  methods: {

    closeByEvent() {
                this.$modal.hide('demo-registro-doc')
    },
      scrollHanle(evt) {
      console.log(evt)
    },
    //...mapActions(['iniciarUsuario']),

    registrarDoctor(doctor, doctorDatos, doctorProfesion) {
      this.carga2=true
      this.doctor = doctor;
      this.doctorDatos = doctorDatos;
      this.doctorProfesion = doctorProfesion;

      this.axios
        .post("https://proyectocalidad9.herokuapp.com/doctor/registro", {
          ...this.doctor,
          ...this.doctorDatos,
          ...this.doctorProfesion
        }) //elemento spreat
        //agrega al obejto json al contenido que agregamos, seria como un solo json de todos los parámetros

        .then(res => {
          this.carga = true;
          this.$modal.hide('demo-registro-doc')
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

.label {
    width: 100%;
    height: 100%;
    font-size: 13px;
    color:  #494949;
    font-weight: bold;
  }
  

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
