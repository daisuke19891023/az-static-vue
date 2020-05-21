<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <h3>test script</h3>
    <h3>{{ message }}</h3>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

type ApiResponse = {
  message: string;
};

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
  message = "";
  async created() {
    console.log(process.env);
    const res = await fetch("/api/hello?name=VueTypescript!!!");
    if (res.ok) {
      const responseMassage = (await res.json()) as ApiResponse;
      console.log(responseMassage);
      this.message = responseMassage.message;
    } else {
      this.message = "failed";
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
