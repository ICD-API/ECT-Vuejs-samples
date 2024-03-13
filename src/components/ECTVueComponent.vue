<template>
  <div>
    <h1>Vue.js v3.4 + ECT v1.7</h1>
    Type for starting search:
    <!-- input element used for typing the search  -->
    <input
      type="text"
      class="ctw-input"
      autocomplete="off"
      v-bind:data-ctw-ino="iNo"
    />
    <!-- div element used for showing the search results -->
    <div class="ctw-window" v-bind:data-ctw-ino="iNo"></div>
  </div>
</template>

<script>
// import the ECT package and style
import * as ECT from '@whoicd/icd11ect';
import '@whoicd/icd11ect/style.css';

export default {
  name: 'ECTVueComponent',
  data() {
    return {
      iNo: 1,
    };
  },
  created() {
    // configure the ECT
    const settings = {
      // the API located at the URL below should be used only for software development and testing
      apiServerUrl: 'https://icd11restapi-developer-test.azurewebsites.net',
      autoBind: false, // in Vue.js we recommend using the manual binding
    };
    const callbacks = {
      selectedEntityFunction: (selectedEntity) => {
        // shows an alert with the code selected by the user and then clears the search results
        alert('ICD-11 code selected: ' + selectedEntity.code);
        ECT.Handler.clear(this.iNo);
      },
    };
    ECT.Handler.configure(settings, callbacks);
  },
  mounted() {
    // manual binding only after the component has been mounted
    ECT.Handler.bind(this.iNo);
  },
};
</script>

<style scoped></style>
