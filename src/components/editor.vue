<template>
  <div>
    <div class="container">
      <div class="editor">
        <quillEditor
          v-model="content"
          ref="myQuillEditor"
          :options="editorOption"
        />
      </div>
    </div>
    <search />
  </div>
</template>

<script>
import { quillEditor } from "vue-quill-editor";
//import { Button, Input, Select } from "iview";
import search from "./search.vue";
export default {
  name: "editor",
  components: {
    // Button,
    // Input,
    // Select,
    quillEditor,
    search,
  },
  data: () => ({
    content: "",
    editorOption: {
      debug: "info",
      placeholder: "Enter here...",
      readOnly: true,
      theme: "snow",
    },
  }),
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  border-color: cadetblue;
  margin-top: 100px;
  border-style: solid;
  border-width: 25px;
  border-radius: 30px;
}
</style>
