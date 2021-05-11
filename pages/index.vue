<template>
  <div class="container">
    <div>
      <h1 class="title">
        Announcements
      </h1>
      <form name="announcements">
        <label for="title">Title</label> <br />
        <input type="text" v-model="state.title" />
        <br />
        <label for="description">Description</label> <br />
        <input type="text" v-model="state.description" />
        <br /><br />
      </form>
      <button type="submit" @click.prevent="submitForm()">Submit</button>
    </div>
  </div>
</template>

<script>
import { reactive, toRefs } from "@vue/composition-api";

export default {
  data() {
    return {
      state: {
        title: "",
        description: ""
      }
    };
  },
  methods: {
    submitForm() {
      console.log(JSON.stringify(this.state));
      fetch("/netlify/functions/save", {
        method: "POST",
        body: this.state
      }).then(res => res.json());
    }
  }
  // setup() {
  //   const state = reactive({
  //     title: "",
  //     description: ""
  //   });
  //   const submitForm = async () => {
  //     const res = await fetch("../netlify/functions/save", {
  //       method: "POST",
  //       body: JSON.stringify(state)
  //     });
  //     const content = await res.json();
  //     console.log(content);
  //   };
  //   return {
  //     ...toRefs(state),
  //     submitForm
  //   };
  // }
};
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
