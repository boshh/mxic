<template>
  <v-app>
    <Bar />

    <v-main>
      <v-container>
        <!-- <HelloWorld/> -->
        <v-row class="text-center">
          <v-col cols="3">
            <MenuBar />
          </v-col>
          <v-col cols="9">
            <Content />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
import Bar from "./components/Bar";
import Content from "./components/Content";
import MenuBar from "./components/MenuBar";

export default {
  name: "App",

  components: {
    Bar,
    Content,
    MenuBar,
  },

  data: () => ({
    //
  }),
};
</script>
