<template>
  <div class="card_wide" id="router_component">
    <h2>
      Router
      <a v-on:click="append_router">add</a>
      /
      <a v-on:click="remove_router">del</a>
    </h2>
    <table v-for="(router, index) in routers" :key="index" style="border:1px solid gray">
      <tr>
        <td>
          <h4>name</h4>
          <input type="text" :value="router.router_config_name" />
        </td>
        <td>
          <h4>
            match rules
            <a v-on:click="append_internal_router" :id="index">add</a>
            /
            <a v-on:click="remove_internal_router" :id="index">del</a>
          </h4>
          <div v-for="(vhost, index) in router.virtual_hosts" :key="index" class="vhost_block">
            <label>host name</label>
            <input type="text" :value="vhost.name" />
            <label>host domain</label>
            <input type="text" :value="vhost.domains" />
            <div v-for="(r, index) in vhost.routers" :key="index">
              <label>match</label>
              <input type="text" :value="r.match" />
              <label>route</label>
              <input type="text" :value="r.route.cluster_name" />
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "#router_component",
  data() {
    return {
      routers: [
        {
          router_config_name: "serverRouter",
          virtual_hosts: [
            {
              name: "serverHost",
              domains: '["*"]',
              routers: [
                {
                  match: '{"prefix" : "/"}', // 还可能有其它结果
                  route: { cluster_name: "serverCluster" },
                },
              ],
            },
          ],
        },
      ],
    };
  },
  methods: {
    //------- router start
    append_router: function (event) {
      this.routers.push({
        router_config_name: "serverRouter",
        virtual_hosts: [
          {
            name: "serverHost",
            domains: '["*"]',
            routers: [
              {
                match: '{"prefix" : "/"}', // 还可能有其它结果
                route: { cluster_name: "serverCluster" },
              },
            ],
          },
        ],
      });
    },
    remove_router: function (event) {
      this.routers.pop();
    },
    append_internal_router: function (event) {
      this.routers[event.target.id].virtual_hosts.push({
        name: "serverHost",
        domains: '["*"]',
        routers: [
          {
            match: '{"prefix" : "/"}', // 还可能有其它结果
            route: { cluster_name: "serverCluster" },
          },
        ],
      });
    },
    remove_internal_router: function (event) {
      this.routers[event.target.id].virtual_hosts.pop();
    },
    //------- router end
  },
};
</script>