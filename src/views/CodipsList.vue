<template>
  <div class="codips-list-containet">
    <AddCodips @showData="showData" />
    <div class="codips-block">
      <Codips
        v-for="(codips, index) in codipses"
        :key="index"
        :codipsData="codips"
        @removeCodips="removeCodips"
      />
    </div>
  </div>
</template>

<script>
import AddCodips from "@/components/AddCodips";
import Codips from "@/components/Codips";

export default {
  name: "CodipsList",
  components: {
    Codips,
    AddCodips
  },
  data() {
    return {
      codipses: [],
      selectedNoteType: "",
      noteTypes: [
        {
          id: 1,
          noteType: "HTML"
        },
        {
          id: 2,
          noteType: "CSS"
        },
        {
          id: 3,
          noteType: "JS"
        }
      ]
    };
  },
  methods: {
    showData(data) {
      console.log("data recieved");
      this.codipses.unshift(data);
      console.log(this.codipses);
    },
    removeCodips(id) {
      const codipsToDelete = this.codipses.findIndex(
        codips => codips.id === id
      );
      this.codipses.splice(codipsToDelete, 1);
    }
  }
};
</script>

<style lang="scss" scoped>
.codips-list-containet {
  width: 100%;
  .add-code-note-form {
    width: 50%;
    form {
      display: flex;
      flex-direction: column;
    }
  }

  .codips-block {
    display: flex;
    flex-wrap: wrap;
  }
}
</style>