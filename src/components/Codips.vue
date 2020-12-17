<template>
  <div class="codips-container">
    <div class="codips-card">
      <div class="codips-card__menu">
        <ul>
          <li>
            <button>e</button>
          </li>
          <li>
            <button @click="removeCodips">d</button>
          </li>
        </ul>
      </div>
      <div
        class="codips-card__title codip-card__item"
      >
        <h1>{{codipsData.title}}</h1>
      </div>
      <div
        class="codips-card__code codip-card__item"
      >
        <p>{{codipsData.code}}</p>
        <p>{{codipsData.id}}</p>
      </div>
      <div
        class="codips-card__description codip-card__item"
      >
        <p>{{codipsData.description}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Codips",
  props: {
    codipsData: {
      type: Object,
      required: true
    }
  },
  methods: {
    removeCodips() {
      console.log(typeof this.codipsData.id);
      this.$emit("removeCodips", this.codipsData.id);
    }
  }
};
</script>

<style lang="scss" scoped>
.codips-container {
  .codips-card {
    position: relative;
    display: flex;
    flex-direction: column;
    width: 250px;
    margin: 15px;
    border-radius: 10px;
    box-shadow: 0 1px 4px silver;

    &__menu {
      position: absolute;
      top: -5px;
      right: 1px;
      // border: 1px solid red;
      ul {
        // border: 1px solid red;
        display: flex;
        justify-content: flex-end;
        list-style-type: none;
        // margin-right: 15px;
        li {
          padding: 0 10px;
          button {
            border: 1px solid silver;
            border-radius: 50%;
            cursor: pointer;
            outline: none;

            &:hover {
              background: #fff;
            }

            &:active {
              transform: scale(0.95);
            }
          }
        }
      }
    }

    &__title {
      border-bottom: 1px solid silver;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    &__code,
    &__description {
      margin: 10px;
      padding: 0 5px;
      box-shadow: 0 1px 4px silver;
      text-align: left;
      border-radius: 5px;
    }

    &__description {
    }
  }
}
</style>