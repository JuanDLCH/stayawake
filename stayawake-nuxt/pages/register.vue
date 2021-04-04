<template>
  <div>
      <h1>Registro</h1>

    <template>
    <v-form ref="formRegister" v-model="valid" lazy-validation>

        <v-text-field 
            v-model="product.id"
            :rules="rules.required"
            label="Identificación" 
         ></v-text-field>

        <v-text-field 
            v-model="product.name"
            :rules="rules.required"
            label="Nombre"
             required
         ></v-text-field>

        <v-text-field 
            v-model="product.lastName"
            :rules="rules.required"
            label="Apellidos" 
            required
        ></v-text-field>  

        <v-text-field 
            v-model="product.mail"
            :rules="rules.required"
            label="E-mail" 
            required
        ></v-text-field>

        <v-text-field 
            v-model="product.password"
            :rules="rules.required"
            label="Contraseña" 
            required
        ></v-text-field>

        <v-btn color="success" @click="saveProduct()">Guardar producto</v-btn>

    </v-form>
    </template>
  </div>
</template>

<script>
  export default {
    data: () => ({
      valid: true,
      product:{
        id: "",
        name: ""
      },
      rules:{
          required: [v => !!v || "El campo es obligatorio"]
      }
    }),

    methods: {
     async saveProduct(){
          if(this.$refs.formRegister.validate()){
            let product = Object.assign({}, this.product); 
            console.log(product);

            //json-server --watch db.json -p 3001

            let response = await this.$axios.post('http://localhost:3001/usuarios', product);
            console.log(response);
          }else{
            console.log("Formualario incompleto");
          } 
      },
      validate () {
        this.$refs.form.validate()
      },
      reset () {
        this.$refs.form.reset()
      },
      resetValidation () {
        this.$refs.form.resetValidation()
      },
    },
  }
</script>

<style>

</style>