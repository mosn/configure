<template>
  <div class="card_wide">
    <h2>
      Listener
      <a v-on:click="append_listener">add</a>
      /
      <a v-on:click="remove_listener">del</a>
    </h2>
    <div v-for="(listener,i) in listeners" :key="listener.name+i" style="border:1px solid gray">
      <table>
        <tr>
          <td>
            <h4>name</h4>
            <input type="text" :value="listener.name" />
          </td>
          <td>
            <h4>address</h4>
            <input type="text" :value="listener.address" />
          </td>
          <td>
            <h4>bind port</h4>
            <input type="text" :value="listener.bind_port" />
          </td>
        </tr>
      </table>
      <table>
        <th>
          network filters
          <a v-on:click="append_network_filter" :id="i">add filter</a>
          /
          <a v-on:click="remove_network_filter" :id="i">del filter</a>
        </th>
        <tr v-for="(filter,idx) in listener.network_filters" :key="filter+idx">
          <td>
            <h4>filter_type</h4>
            <input type="text" :value="filter.type" />
          </td>
          <td>
            <h4>downstream_protocol</h4>
            <input type="text" :value="filter.config.downstream_protocol" />
          </td>
          <td>
            <h4>upstream_protocol</h4>
            <input type="text" :value="filter.config.upstream_protocol" />
          </td>
          <td>
            <h4>router name</h4>
            <input type="text" :value="filter.config.router_config_name" />
          </td>
        </tr>
      </table>
      <table>
        <th>
          listener filters
          <a v-on:click="append_listener_filter" :id="i">add filter</a>
          /
          <a v-on:click="remove_listener_filter" :id="i">del filter</a>
        </th>
        <tr></tr>
      </table>
      <table>
        <th>
          stream filters
          <a v-on:click="append_stream_filter" :id="i">add filter</a>
          /
          <a v-on:click="remove_stream_filter" :id="i">del filter</a>
        </th>
        <tr></tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "#router_component",
  data() {
    return {
      listeners: [
        {
          name: "serverListener",
          address: "127.0.0.1:2045",
          bind_port: true,
          listener_filters: [],
          stream_filters: [],
          network_filters: [
            {
              type: "proxy",
              config: {
                downstream_protocol: "Http1",
                upstream_protocol: "Http1",
                router_config_name: "serverRouter",
              },
            },
          ],
        },
      ],
    };
  },
  methods: {
    append_listener: function (event) {
      this.listeners.push({
        name: "serverListener",
        address: "127.0.0.1:2045",
        bind_port: true,
        listener_filters: [],
        stream_filters: [],
        network_filters: [
          {
            type: "proxy",
            config: {
              downstream_protocol: "Http1",
              upstream_protocol: "Http1",
              router_config_name: "serverRouter",
            },
          },
        ],
      });
    },
    remove_listener: function (event) {
      this.listeners.pop();
    },
    append_network_filter: function (event) {
      this.listeners[event.target.id].network_filters.push({
        type: "proxy",
        config: {
          downstream_protocol: "Http1",
          upstream_protocol: "Http1",
          router_config_name: "serverRouter",
        },
      });
    },
    remove_network_filter: function (event) {
      this.listeners[event.target.id].network_filters.pop();
    },
    append_stream_filter: function (event) {},
    remove_stream_filter: function (event) {},
    append_listener_filter: function (event) {},
    remove_listener_filter: function (event) {},
  },
};
</script>
