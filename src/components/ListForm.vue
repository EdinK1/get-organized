<template>
  <form class="form">
    <h3 class="form-title">Create a new one 📎</h3>
    <input
      placeholder="Do Yoga 🧘‍♀️"
      class="input"
      type="text"
      name="title"
      id="title"
    />
    <textarea
      placeholder="Stretch it girl 💪"
      rows="5"
      class="input"
      name="desc"
      id="desc"
    ></textarea>
    <button class="create-button" type="submit">Create</button>
  </form>
</template>

<script>
export default {
  methods: {}
}
</script>

<style scoped>
.form {
  padding: 1rem;
  margin: 2rem 0;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  max-width: 600px;
  width: 90%;
  margin: 0 auto;
}

.form-title {
  font-size: 1.25rem;
  color: #333;
  font-weight: 200;
}

.input {
  padding: 1rem 0;
  font-size: 1.05rem;
  margin: 1rem 0;
  width: 100%;
  border: none;
  border-bottom: 0.4px solid #333;
}

.create-button {
  background-color: #b3893a;
  border: none;
  color: #fff;
  padding: 0.5rem 1.5rem;
  font-size: 1.05rem;
  transition: background 0.4s ease-in-out;
  cursor: pointer;
}

.create-button:hover {
  background-color: #c0923c;
}
</style>
