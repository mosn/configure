<template>
  <div class="card_wide">
    <h2>
      Listener
      <a v-on:click="append_listener">add</a>
      /
      <a v-on:click="remove_listener">del</a>
    </h2>
    <div v-for="(listener,i) in listeners" :key="listener.name" style="border:1px solid gray">
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
          filter chain
          <a v-on:click="append_filter_chain" :id="i">add</a>
          /
          <a v-on:click="remove_filter_chain" :id="i">del</a>
        </th>
        <tr v-for="(chain, index) in listener.filter_chains" :key="index">
          <h4>
            chain {{index}}
            <a v-on:click="append_filter" :id="i" :name="index">add filter</a>
            /
            <a v-on:click="remove_filter" :id="i" :name="index">del filter</a>
          </h4>
          <div v-for="filter in chain.filters" :key="filter.index" style="border:1px solid gray">
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
          </div>
        </tr>
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
          filter_chains: [
            // network filters
            {
              filters: [
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
        filter_chains: [
          {
            filter: [
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
      });
    },
    remove_listener: function (event) {
      this.listeners.pop();
    },
    append_filter_chain: function (event) {
      this.listeners[event.target.id].filter_chains.push({
        filter: [
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
    append_filter: function (event) {
      this.listeners[event.target.id].filter_chains[
        event.target.name
      ].filters.push({
        type: "proxy",
        config: {
          downstream_protocol: "Http1",
          upstream_protocol: "Http1",
          router_config_name: "serverRouter",
        },
      });
    },
    remove_filter: function (event) {
      this.listeners[event.target.id].filter_chains[
        event.target.name
      ].filters.pop();
    },
    remove_filter_chain: function (event) {
      this.listeners[event.target.id].filter_chains.pop();
    },
  },
};
</script>
