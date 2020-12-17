<template>
  <div class="add-codips-container">
    <button
      class="add-codips__form-opener"
      @click="isAddCodipsFormOpen=!isAddCodipsFormOpen"
      v-show="!isAddCodipsFormOpen"
    >+</button>
    <button
      class="add-codips__form-closer"
      @click="isAddCodipsFormOpen=!isAddCodipsFormOpen"
      v-show="isAddCodipsFormOpen"
    >Х</button>
    <div
      class="add-codips__form"
      v-show="isAddCodipsFormOpen"
    >
      <form>
        <label
          for="add-codips__title"
        >Codips Title</label>
        <input
          type="text"
          id="add-codips__title"
          class="add-codips__title"
          v-model="codipsData.title"
        />
        <label for="codips__code">Code</label>
        <textarea
          type="textarea"
          rows="4"
          id="codips__code"
          v-model="codipsData.code"
        />
        <label
          for="codips__description"
        >Description</label>
        <textarea
          type="textarea"
          id="codips__description"
          v-model="codipsData.description"
        />
        <label for="codips__type">Code Note Type</label>
        <!-- <select>
          <option
            v-for="option in noteTypes"
            :key="option.id"
            :value="option.noteType"
          >{{option.noteType}}</option>
        </select>-->
        <!-- <h2>{{selectedNoteType}}</h2> -->
        <button
          class="add-codips__add-button"
          @click.prevent="emitDataToParent"
        >Add</button>
      </form>
      {{codipsId}}
    </div>
  </div>
</template>

<script>
export default {
  name: "AddCodips",
  data() {
    return {
      isAddCodipsFormOpen: false,
      codipsId: "",
      codipsData: {
        title: "",
        code: "",
        description: ""
      },
      title: ""
    };
  },
  methods: {
    emitDataToParent() {
      const data = this.codipsData;
      if (data.title && data.code) {
        this.codipsId++;
        const dataToSend = JSON.parse(JSON.stringify(data));
        dataToSend.id = this.codipsId;
        this.$emit("showData", dataToSend);
        Object.keys(data).forEach(key => (data[key] = ""));
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.add-codips-container {
  width: 400px;
  margin: 15px;
  button {
    width: 50px;
    height: 50px;
    border: 1px solid silver;
    border-radius: 50%;
    box-shadow: 0 1px 4px silver;
    font-size: 2.3rem;
    color: silver;
    margin-bottom: 15px;
    cursor: pointer;
    transition: transform 200ms ease;

    &:hover {
      // box-shadow: 0 0 2px silver;
      color: rgb(153, 153, 255);
    }

    &:active {
      transform: scale(0.9);
    }
  }

  .add-codips__form-closer {
    font-size: 1.5rem;
  }

  .add-codips__form {
    box-shadow: 0 1px 4px silver;

    form {
      display: flex;
      flex-direction: column;
      margin: 10px;

      input,
      textarea {
        border: none;
        box-shadow: 0 1px 4px silver;
      }

      .add-codips__add-button {
        font-size: 1rem;
      }
    }
  }
}
</style>