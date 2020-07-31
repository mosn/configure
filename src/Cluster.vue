<template>
  <div class="card_wide" id="cluster_component">
    <h2>
      Cluster
      <a v-on:click="append_cluster" :id="index">add</a>
      /
      <a v-on:click="remove_cluster" :id="index">del</a>
    </h2>
    <table v-for="(cluster,index) in clusters" :key="index" style="border:1px solid gray">
      <tr>
        <td>
          <h4>name</h4>
          <input type="text" :value="cluster.name" />
        </td>
        <td>
          <h4>type</h4>
          <input type="text" :value="cluster.type" />
        </td>
        <td>
          <h4>lb_type</h4>
          <input type="text" :value="cluster.lb_type" />
        </td>
        <td>
          <h4>max_request_per_conn</h4>
          <input type="text" :value="cluster.max_request_per_conn" />
        </td>
        <td>
          <h4>conn_buffer_limit_bytes</h4>
          <input type="text" :value="cluster.conn_buffer_limit_bytes" />
        </td>
      </tr>
      <tr>
        <td>
          <h4>
            address list:
            <a v-on:click="add_addr_to_cluster" :id="index">add</a>
            /
            <a v-on:click="remove_addr_to_cluster" :id="index">del</a>
          </h4>
          <input
            class="addr_box"
            type="text"
            v-for="item in cluster.hosts"
            :key="item.address"
            :value="item.address"
          />
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "#cluster_component",
  data() {
    return {
      clusters: [
        {
          name: "serverCluster",
          type: "SIMPLE",
          lb_type: "LB_RANDOM",
          max_request_per_conn: 1024,
          conn_buffer_limit_bytes: 32768,
          hosts: [{ address: "127.0.0.1:8080" }],
        },
      ],
    }
  },
  methods : {
    //------- cluster start
    add_addr_to_cluster: function (event) {
      this.clusters[event.target.id].hosts.push({ address: "127.0.0.1:8080" });
    },
    remove_addr_to_cluster: function (event) {
      this.clusters[event.target.id].hosts.pop();
    },
    append_cluster: function (event) {
      this.clusters.push({ hosts: [{ address: "127.0.0.1:8080" }] });
    },
    remove_cluster: function (event) {
      this.clusters.pop();
    },
    //------- cluster end
  }
}
</script>