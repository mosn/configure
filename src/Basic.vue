<template>
<div id = "basic_component">
    <div class="card">
      <h2>Log</h2>
      <h4>Log Level</h4>
      <select v-model="log.level">
        <option value="INFO">INFO</option>
        <option value="ERROR">ERROR</option>
        <option value="DEBUG">DEBUG</option>
      </select>
      <br />
      <h4>Log Path</h4>
      <input type="text" :value="log.path" />
    </div>
    <div class="card">
      <h2>Admin</h2>
      <h4>IP</h4>
      <p>
        <input type="text" :value="admin.address" />
      </p>
      <h4>Port</h4>
      <input type="text" :value="admin.port_value" />
    </div>
    <div class="card">
      <h2>Tracing</h2>
      <h4>Enable</h4>
      <p>
        <input type="text" :value="tracing.enable" />
      </p>
      <h4>Driver</h4>
      <input type="text" :value="tracing.driver" />
    </div>
    <div class="card">
      <h2>PProf</h2>
      <h4>Enable</h4>
      <p>
        <input type="text" :value="pprof.debug" />
      </p>
      <h4>Port</h4>
      <input type="text" :value="pprof.port_value" />
    </div>
</div>
</template>

<script>
export default {
  name: "#basic_component",
  data() {
    return {
      log: {
        level: "INFO",
        path: "/tmp/test.log"
      },
      admin: {
        address: "0.0.0.0",
        port_value: 12345
      },
      tracing: {
        enable: false,
        driver: "SOFATracer"
      },
      pprof: {
        debug: true,
        port_value: 34092
      },
    }
  }
}
</script>

<style scoped>
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
</style>