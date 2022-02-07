<template>
  <b-card 
      class="mb-0" >
    <validation-observer ref="simpleRules">
      <b-form>
        <b-row>

          <!--  This field is required-->
          <b-col md="6">
            <b-form-group>
              <label>Ingrese sus Nombres</label>
              <validation-provider
                #default="{ errors }"
                rules="required"
                name="Nombres"
              >
                <b-form-input
                  v-model="name"
                  :state="errors.length > 0 ? false:null"
                  placeholder="Nombres"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </validation-provider>
            </b-form-group>
          </b-col>
          <b-col md="6">
            <b-form-group>
              <label>Ingrese su Apellido Paterno</label>
              <validation-provider
                #default="{ errors }"
                rules="required"
                name="Apellido Paterno"
              >
                <b-form-input
                  v-model="apellidoP"
                  :state="errors.length > 0 ? false:null"
                  placeholder="Apellido Paterno"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </validation-provider>
            </b-form-group>
          </b-col>
          <b-col md="6">
            <b-form-group>
              <label>Ingrese su Apellido Materno</label>
              <validation-provider
                #default="{ errors }"
                rules="required"
                name="Apellido Materno"
              >
                <b-form-input
                  v-model="apellidoP"
                  :state="errors.length > 0 ? false:null"
                  placeholder="Apellido Materno"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </validation-provider>
            </b-form-group>
          </b-col>
          <!-- fecha de nacimiento falta validar que este-->
          <b-col md="6">
            <b-form-group>
              <label> Ingrese su fecha de nacimiento</label>
              <b-form-datepicker
                v-model="value"
                :min="min"
                :max="max"
                locale="es"
              />
            </b-form-group>
          </b-col>
          <!-- rut falta arreglar validacion -->
          <b-col md="6">
            <b-form-group>
              <label>Ingrese su Rut</label>
              <validation-provider
                #default="{ errors }"
                rules="required|digits:9"
                name="Numeric"
              >
                <b-form-input
                  v-model="digitValue2"
                  :state="errors.length > 0 ? false:null"
                  placeholder="Rut"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </validation-provider>
            </b-form-group>
          </b-col>

          <!-- direccion -->
          <b-col md="6">
            <b-form-group>
              <label>Ingrese su Dirección </label>
              <validation-provider
                #default="{ errors }"
                rules="required"
                name="Direccion"
              >
                <b-form-input
                  v-model="direccion"
                  :state="errors.length > 0 ? false:null"
                  placeholder="Dirección"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </validation-provider>
            </b-form-group>
          </b-col>
        <!-- credencial de discapacidad-->
        <b-col md="6">
          <b-form-group>
            <label for=""> ¿Cuenta con credencial de Discapacidad? </label>
            <v-select
              v-model="selected1"
              :dir="$store.state.appConfig.isRTL ? 'rtl' : 'ltr'"
              label="title"
              placeholder="selecciona"
              :options="option"
            />
          </b-form-group>
        </b-col>
        <!-- tipo de discapacidad-->
        <b-col md="6">
          <b-form-group>
            <label for=""> Tipo de Discapacidad </label>
            <v-select
                v-model="selected2"
                :dir="$store.state.appConfig.isRTL ? 'rtl' : 'ltr'"
                multiple
                label="title"
                placeholder="elige una o mas"
                :options="option2"
              />
          </b-form-group>
        </b-col>
          <!-- nivel educacional-->
        <b-col md="6">
          <b-form-group>
            <label for=""> Nivel educacional </label>
            <v-select
              v-model="selected3"
              :dir="$store.state.appConfig.isRTL ? 'rtl' : 'ltr'"
              label="title"
              placeholder="selecciona"
              :options="option3"
            />
          </b-form-group>
        </b-col>
        <!--espacio vacio-->
        <b-col md="6">

        </b-col>
        <!-- registro social pregunta-->
        <b-col md="6">
          <b-form-group>
            <label for=""> ¿Cuenta con Registro Social de Hogares? </label>
            <v-select
              v-model="seleccionRegistro"
              :dir="$store.state.appConfig.isRTL ? 'rtl' : 'ltr'"
              label="title"
              placeholder="selecciona"
              :options="option"
            />
          </b-form-group>
        </b-col>
        <!-- menu if Si-->
        <b-col md="6" v-if="seleccionRegistro.title==='Si'">
          <b-form-group>
            <label for=""> Calificación Socio-Económica según Registro Social de Hogares </label>
            <v-select
              v-model="seleccionRegistro2"
              :dir="$store.state.appConfig.isRTL ? 'rtl' : 'ltr'"
              label="title"
              placeholder="selecciona"
              :options="opcionRegistro2"
            />
          </b-form-group>
        </b-col>
        <!--menu if No-->
        <b-col md="6" v-else></b-col>
        <!--recibe beneficio pregunta-->
        <b-col md="6">
          <b-form-group>
            <label for=""> ¿Recibe algún beneficio? </label>
            <v-select
              v-model="seleccionBeneficio"
              :dir="$store.state.appConfig.isRTL ? 'rtl' : 'ltr'"
              label="title"
              placeholder="selecciona"
              :options="option"
            />
          </b-form-group>
        </b-col>
        <!-- seleccion beneficio if Si-->
        <b-col md="6" v-if="seleccionBeneficio.title==='Si'">
            <b-form-group>
              <label>Ingrese el nombre de los beneficios que recibe</label>
              <validation-provider
                #default="{ errors }"
                rules="required"
                name="Benefio que recibe"
              >
                <b-form-input
                  v-model="beneficio"
                  :state="errors.length > 0 ? false:null"
                  placeholder=""
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </validation-provider>
            </b-form-group>
        </b-col>
        <!--if No-->
        <b-col md="6" v-else></b-col>
        <!--establecimiento educacional pregunta-->
        <b-col md="6">
          <b-form-group>
            <label for=""> ¿Es alumno de algún establecimiento educacional actualmente? </label>
            <v-select
              v-model="seleccionEstablecimiento"
              :dir="$store.state.appConfig.isRTL ? 'rtl' : 'ltr'"
              label="title"
              placeholder="seleccione"
              :options="option"
            />
          </b-form-group>
        </b-col>
        <!-- seleccion beneficio if Si-->
        <b-col md="6" v-if="seleccionEstablecimiento.title==='Si'">
            <b-form-group>
              <label>Ingrese el nombre del Establecimiento</label>
              <validation-provider
                #default="{ errors }"
                rules="required"
                name="Establecimiento Educacional"
              >
                <b-form-input
                  v-model="establecimiento"
                  :state="errors.length > 0 ? false:null"
                  placeholder="Establecimiento Educacional"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </validation-provider>
            </b-form-group>
        </b-col>
        <!--if No-->
        <b-col md="6" v-else></b-col>
        <!--trabajo pregunta-->
        <b-col md="6">
          <b-form-group>
            <label for=""> ¿Se encuentra trabajando actualmente?  </label>
            <v-select
              v-model="seleccionTrabajo"
              :dir="$store.state.appConfig.isRTL ? 'rtl' : 'ltr'"
              label="title"
              placeholder="seleccione"
              :options="option"
            />
          </b-form-group>
        </b-col>
        <!-- seleccion beneficio if Si-->
        <b-col md="6" v-if="seleccionTrabajo.title==='Si'">
            <b-form-group>
              <label>Ingrese el nombre de su lugar de trabajo</label>
              <validation-provider
                #default="{ errors }"
                rules="required"
                name="Lugar de Trabajo"
              >
                <b-form-input
                  v-model="trabajo"
                  :state="errors.length > 0 ? false:null"
                  placeholder="Lugar de Trabajo"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </validation-provider>
            </b-form-group>
        </b-col>
        <!--if No-->
        <b-col md="6" v-else></b-col>
        <!--Cuiador pregunta-->
        <b-col md="6">
          <b-form-group>
            <label for=""> ¿Cuidador?  </label>
            <v-select
              v-model="seleccionCuidador"
              :dir="$store.state.appConfig.isRTL ? 'rtl' : 'ltr'"
              label="title"
              placeholder="seleccione"
              :options="option"
            />
          </b-form-group>
        </b-col>
        <!-- seleccion beneficio if Si-->
        <b-col md="6" v-if="seleccionCuidador.title==='Si'">
            <b-form-group>
              <label>Ingrese el nombre y apellido de su cuidador</label>
              <validation-provider
                #default="{ errors }"
                rules="required"
                name="Nombre y Apellido Cuidador"
              >
                <b-form-input
                  v-model="cuidador"
                  :state="errors.length > 0 ? false:null"
                  placeholder="Nombre y Apellido Cuidador"
                />
                <small class="text-danger">{{ errors[0] }}</small>
              </validation-provider>
            </b-form-group>
        </b-col>
        <!--if No-->
        <b-col md="6" v-else></b-col>



          <!-- submit button -->
          <b-col cols="12">
            <b-button
              variant="primary"
              type="submit"
              @click.prevent="validationForm"
            >
              Submit
            </b-button>
          </b-col>
        </b-row>
      </b-form>
    </validation-observer>
  </b-card>
</template>

<script>
import { ValidationProvider, ValidationObserver } from 'vee-validate'
import {
  BCard, BFormDatepicker, BFormInput, BFormGroup, BForm, BRow, BCol, BButton,
} from 'bootstrap-vue'
import {
  required, email, confirmed, url, between, alpha, integer, password, min, digits, alphaDash, length,
} from '@validations'
import vSelect from 'vue-select'

export default {
  components: {
    BCard,
    vSelect,
    BFormDatepicker,
    ValidationProvider,
    ValidationObserver,
    BFormInput,
    BFormGroup,
    BForm,
    BRow,
    BCol,
    BButton,
  },
  data() {
    const now = new Date()
    const today = new Date(now.getFullYear(), now.getMonth(), now.getDate())
    // 15th two months prior
    const minDate = new Date(today)
    minDate.setMonth(minDate.getMonth() - 2)
    minDate.setDate(15)
    // 15th in two months
    const maxDate = new Date(today)
    maxDate.setMonth(maxDate.getMonth())
    maxDate.setDate(maxDate.getDate())
    return {
      nombreCuidador: '',
      seleccionCuidador: '',
      trabajo: '',
      seleccionTrabajo:'',
      seleccionEstablecimiento: '',
      establecimiento: '',
      beneficio: '',
      seleccionBeneficio: '',
      seleccionRegistro2:'',
      opcionRegistro2: [
        {title: '40%'},
        {title: '50%'},
        {title: '60%'},
        {title: '70%'},
        {title: '80%'},
        {title: '90%'},
        {title: '100%'},
        ],
      seleccionRegistro:'',
      registro: '',
      selected1: '',
      option: [{ title: 'Si' }, { title: 'No' }],
      selected2: '',
      option2: [
        {title: 'Discapacidad Física'},
        {title: 'Discapacidad Sensorial Visual'},
        {title: 'Discapacidad Mental/Psíquica'},
        {title: 'Discapacidad Mental/ Intelectual'},],
      dir: 'ltr',
      selected3:[],
      option3:[
        {title: 'Nivel preescolar'},
        {title: 'Enseñanza básica completa'},
        {title: 'Enseñanza básica incompleta'},
        {title: 'Enseñanza media completa'},
        {title: 'Enseñanza media incompleta'},
        {title: 'Enseñanza Técnica Superior Completa'},
        {title: 'Enseñanza Técnica Superior Incompleta'},
        {title: 'Educación Universitaria completa'},
        {title: 'Educación Universitaria incompleta'},
      ],
      direccion: '',
      value: '',
      min: minDate,
      max: maxDate,
      name: '',
      apellidoP: '',
      apellidoM: '',
      digitValue2: '',
      required,
      confirmed,
      password,
      email,
      min,
      integer,
      url,
      alpha,
      between,
      digits,
      length,
      alphaDash,
    }
  },
  methods: {
    validationForm() {
      this.$refs.simpleRules.validate().then(success => {
        if (success) {
          // eslint-disable-next-line
          alert('form submitted!')
        }
      })
    },
  },
}
</script>
<style lang="scss">
@import '~@core/scss/vue/libs/vue-select.scss';
</style>