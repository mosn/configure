<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <hr />
    <basic_component />
    <hr />

    <h2>stream direction : listener -> router -> cluster</h2>
    <cluster_component />

    <!-- router start -->
    <router_component />
    <!-- router end -->
    <hr />

    <!-- listener start -->
    <listener_component />
    <!-- listener end -->
    <hr />

    <button v-on:click="generate_json">Generate JSON</button>
    <hr />
    <div>
      <input type="text" class="json_box" :value="json_data" />
    </div>
  </div>
</template>

<script>
import basic_component from "./Basic";
import cluster_component from "./Cluster";
import router_component from "./Router";
import listener_component from "./Listener";

export default {
  name: "app",
  components: {
    basic_component,
    cluster_component,
    router_component,
    listener_component,
  },
  data() {
    return {
      msg: "MOSN configuration generator",
      json_data: "",
    };
  },
  methods: {
    generate_json: function (event) {
      alert(basic_component.data().log.path);
      var x = {
        log: this.log,
        admin: this.admin,
        tracing: this.tracing,
        pprof: this.pprof,
        listeners: this.clusters,
        cluster: this.clusters,
        router: this.current_router,
      };
      this.json_data = JSON.stringify(x);
    },
  },
};
</script>

<style>
.vhost_block {
  border: 1px solid gray;
  padding: 3px;
}

td {
  padding: 10px;
}

h4 {
  font-size: 20px;
}

.addr_box {
  display: block;
}

#copy_text {
  width: 8%;
  height: 30px;
}

.json_box {
  width: 100%;
  height: auto;
  font-size: 18px;
  padding-left: 12px;
}

.card_wide {
  width: 100%;
  height: auto;
  display: inline-block;
  border: 1px solid gray;
  margin-top: 20px;
  padding: 10px;
}

.card {
  height: 160px;
  padding: 15px;
  text-align: left;
  width: 22%;
  display: inline-block;
}

button {
  width: 100%;
  height: 40px;
  font-size: 20px;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 0px;
  padding: 15px;
}

h1,
h2 {
  font-weight: normal;
  text-align: center;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
