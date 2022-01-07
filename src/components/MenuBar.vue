<template>
  <v-treeview :active.sync="active" :items="items" :load-children="getChildren" :open.sync="open" activatable color="warning" open-on-click>
    <template v-slot:prepend="{ item }">
      <v-icon v-if="!item.children"> mdi-account </v-icon>
    </template>
  </v-treeview>
</template>

<script>
import { MainGroup, SubGroup } from "../comment/Tree";

export default {
  data: () => ({
    active: [],
    avatar: null,
    open: [],
    users: [],
    items: [],
  }),
  created() {
    const data = MainGroup["items"];
    let group = [];
    data.forEach((d, index) => {
      let arr = [];
      if (group.length > 0) {
        arr = group.filter((item) => item.name === d[0]);
      }
      if (arr.length === 0) {
        group.push({ id: `${index}`, name: d[0], children: [{ id: `${index}${1}`, name: d[1], children: [] }] });
      } else {
        arr[0].children.push({ id: `${arr[0].id}${index}`, name: d[1], children: [] });
      }
    });
    this.items = group;
  },

  computed: {
  },

  methods: {
    getChildren(item) {
      const name = item.name;
      SubGroup.items.forEach((d, index) => {
        if (d[1].includes(name) && d[2] === `${item.id}`.length) {
          item.children.push({ id: `${item.id}${index}`, name: d[0], children: [] });
        }
      });
      // return item;
      // // Remove in 6 months and say
      // // you've made optimizations! :)
      // await pause(1500)

      // return fetch('https://jsonplaceholder.typicode.com/users')
      //   .then(res => res.json())
      //   .then(json => (item.children.push(...json)))
      //   .catch(err => console.warn(err))
    },
  },
};
</script>
