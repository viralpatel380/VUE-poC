<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" width="25%"> -->
    <!-- <HelloWorld msg="Hello Vue in CodeSandbox!"/> -->
    <div>
      <h1>Total Questions{{ questions.total }}</h1>
      <input type="text" v-model="questions.total" /> <br />
      <label for="Easy">
        <select
          name="Easy"
          v-model="questions.diff.easy"
          aria-label="Easy"
          id="easy"
        >
          <option v-for="i in parseInt(questions.total)" :value="i" :key="i">
            {{ i }}
          </option>
        </select>
      </label>
      <select name="Mid" v-model="questions.diff.mid" id="easy">
        <option
          v-for="i in parseInt(questions.total) - questions.diff.easy"
          :value="i"
          :key="i"
        >
          {{ i }}
        </option>
      </select>
      <select name="Hard" v-model="questions.diff.hard" id="easy">
        <option
          v-for="i in parseInt(questions.total) -
          (questions.diff.mid + questions.diff.easy)"
          :value="i"
          :key="i"
        >
          {{ i }}
        </option>
      </select>

      <pre>{{ questions.diff }}</pre>
      <code>{{
        questions.diff.head + questions.diff.mid + questions.diff.easy
      }}</code>
    </div>
    <button @click="add()">add</button>
    <button @click="remove()">Remove</button>
    <div class="position: absolute">
      <img
        v-for="i in users"
        :src="`https://api.dicebear.com/7.x/notionists/svg?seed=${Math.random()
          .toString(36)
          .substring(2, 6 + 2)}`"
        class="avatar"
        alt=""
        ref="avatar"
        srcset=""
        :key="i"
        :width="Math.random() * (90 - 10) + 10 || 20"
      />
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
  async mounted() {
    // wait for $refs to be available

    this.$refs.avatar.forEach((avatar) => {
      avatar.style.left =
        Math.random() * (this.$refs.main.clientWidth - avatar.clientWidth) +
        "px";
      avatar.style.top =
        Math.random() * (this.$refs.main.clientHeight - box.clientHeight) +
        "px";
    });
  },

  data() {
    return {
      questions: {
        total: 0,
        diff: {
          hard: 0,
          mid: 0,
          easy: 0,
        },
      },
      users: [1, 2.3, 4],
    };
  },
  methods: {
    add() {
      this.users.push(2);
    },
    remove() {
      this.users.pop(2);
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.avatar {
  border-radius: 100%;
  background-color: lightgoldenrodyellow;
  border: 2px solid rgb(207, 207, 207);
  animation: 0.5s ease-out 0s 1 slideInLeft;
  /* position: absolute; */
}
@keyframes slideInLeft {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(0.3);
  }
}
</style>
