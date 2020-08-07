<template>
  <header>
    <div class="text-box">
      <h1>
        Cat Breeds 🐱
      </h1>
      <p class="mt-3">Different Kinds of Cat Breeds</p>
      <nuxt-link class="btn btn-outline btn-large btn-info" to="/breeds">View Neko Chans</nuxt-link>
    </div>
  </header>
</template>

<script>
export default {
  head() {
    return {
      title: "Home Page"
    };
  },
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

header {
  min-height: 100vh;
  background-image: linear-gradient(
    to right,
    rgba(0,0,0,0.9),
    rgba(0,0,0,0.4)
  ),
  url("/images/banner.jpg");
  background-position: center;
  background-size: cover;
  position: relative;
}

.text-box {
  position: absolute;
  top: 50%;
  left: 10%;
  transform: translateY(-50%);
  color: #fff;
}

.text-box h1 {
  font-family: cursive;
  font-size: 5rem;
}

.text-box p {
  font-size: 2rem;
  font-weight: lighter;
}
</style>
