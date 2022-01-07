<template>
  <form class="Icon-inside" v-on:submit.prevent="handleSearch">
    <input type="text" placeholder="Digite uma cidade" v-model="cityName" required />
    <i class="fa fa-user fa-lg fa-fw" aria-hidden="true">
      <img src="../assets/search-icon.svg" width="15" />
    </i>
  </form>
</template>

<script>
export default ({
  name: 'SearchInput',
  data() {
    return {
      cityName: ''
    }
  },
  methods: {
    handleSearch() {
      this.$emit('city', this.cityName);
    }
  },
})
</script>

<style>
@import "../styles/globalStyles.css";
input {
  background-color: rgba(71, 71, 71, 0.479);
  backdrop-filter: blur(20px);
  color: white;
  width: 30vw;
  height: 6vh;
  padding: 15px;
  margin: 4px;
  box-sizing: border-box;
  border-radius: 0.5rem;
  border: none;
}
input:focus {
  outline: none;
}
.Icon-inside {
  position: relative;
}

.Icon-inside i {
  position: absolute;
  right: 0;
  padding: 14px 12px;
}

@media only screen and (max-width: 600px) {
  input{
    width: 70vw;
  }
}
</style>
