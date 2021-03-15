<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <h1>Form</h1>
    </v-app-bar>

    <v-main>
      <Form />
    </v-main>
  </v-app>
</template>

<script>
import Form from "./components/Form";

export default {
  name: "App",

  components: {
    Form
  },

  data: () => ({
    //
  })
};
</script>
