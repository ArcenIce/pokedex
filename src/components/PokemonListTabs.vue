<template>
  <div class="tabs">
    <button @click="$emit('Previous')">Précédant</button>
    <button @click="$emit('Next')">Suivant</button>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      searched: "",
    }
  }
};
</script>

<style scoped>
.searchbar {
  position: relative;
  width: 100%;
  max-width: 510px;
  padding-bottom: 20px;
}
input {
  border: none;
  outline: none;
  border-radius: 5px;
  padding: 10px 40px 10px 10px;
  width: calc(100% - 50px);
  font-size: 1rem;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}

button {
  background-color: white;
  border-radius: 15px;
  border:0px;
  width: 120px;
  height: 40px;
  margin: 10px;
  margin-top: 20px;
}

button:hover {
  background-color:bisque;
}

button:active {
  background-color: aliceblue;
}
</style>
