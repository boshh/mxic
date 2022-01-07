<template>
  <div>
    <div class="col-12 f-flex align-center" style="text-align: left">Production Data</div>
    <v-card class="col-12" outlined>
      <v-card-title>Imformation</v-card-title>
      <v-row no-gutters>
        <v-col cols="3" class="d-flex align-center">
          <v-row no-gutters>
            <v-col cols="5" class="d-flex align-center justify-center">Car ID</v-col>
            <v-col cols="7" no-gutters>
              <v-text-field placeholder="Production Data" v-model="info['Car ID']" dense outlined hide-details="auto" />
            </v-col>
          </v-row>
        </v-col>
        <v-col cols="3" class="d-flex align-center">
          <v-row no-gutters>
            <v-col cols="5" class="d-flex align-center justify-center">Product ID</v-col>
            <v-col cols="7" no-gutters>
              <v-select dense outlined hide-details="auto" :items="info['Prod ID']">></v-select>
            </v-col>
          </v-row>
        </v-col>
        <v-col cols="3" class="d-flex align-center">
          <v-row no-gutters>
            <v-col cols="5" class="d-flex align-center justify-center">Test Name</v-col>
            <v-col cols="7" no-gutters>
              <v-text-field placeholder="ProdTestName" v-model="info['Test Name']" dense outlined hide-details="auto" />
            </v-col>
          </v-row>
        </v-col>
        <v-col cols="1" class="d-flex align-center pl-2">
          <v-btn color="secondary">Query</v-btn>
        </v-col>
      </v-row>
      <v-tabs v-model="selectTab" class="mt-5">
        <v-tab v-for="(item, index) in tab" :key="index"> {{ item }}</v-tab>
      </v-tabs>
      <v-tabs-items v-model="selectTab">
        <v-tab-item :key="0" class="pl-5">
          <v-row no-gutters class="mt-5">
            <v-col cols="5" class="d-flex align-center">
              <v-row no-gutters>
                <v-col cols="5" class="d-flex align-center justify-left">Type</v-col>
                <v-col cols="7">
                  <v-text-field dense outlined hide-details="auto" v-model="base[0]['Type']"></v-text-field>
                </v-col>
              </v-row>
            </v-col>
            <v-col cols="5" class="d-flex align-center pl-2">
              <v-row no-gutters>
                <v-col cols="5" class="d-flex align-center justify-left">Status</v-col>
                <v-col cols="7">
                  <v-text-field dense outlined hide-details="auto" v-model="base[0]['Status']"></v-text-field>
                </v-col>
              </v-row>
            </v-col>
            <v-col cols="2" class="d-flex align-center pl-2">
              <v-btn color="secondary">Info</v-btn>
            </v-col>
          </v-row>
          <v-row no-gutters class="mt-5">
            <v-col cols="5" class="d-flex align-center">
              <v-row no-gutters>
                <v-col cols="5" class="d-flex align-center justify-left">Sub Type</v-col>
                <v-col cols="7">
                  <v-text-field dense outlined hide-details="auto" v-model="base[0]['Sub Type']"></v-text-field>
                </v-col>
              </v-row>
            </v-col>
            <v-col cols="5" class="d-flex align-center pl-2">
              <v-row no-gutters>
                <v-col cols="5" class="d-flex align-center justify-left">Description</v-col>
                <v-col cols="7">
                  <v-text-field dense outlined hide-details="auto" v-model="base[0]['Description']"></v-text-field>
                </v-col>
              </v-row>
            </v-col>
          </v-row>
          <v-row no-gutters class="mt-5">
            <v-col cols="5" class="d-flex align-center">
              <v-row no-gutters>
                <v-col cols="5" class="d-flex align-center justify-left">Last Claimed TS</v-col>
                <v-col cols="7">
                  <v-text-field dense outlined hide-details="auto" v-model="base[0]['Last Claimed TS']"></v-text-field>
                </v-col>
              </v-row>
            </v-col>
            <v-col cols="5" class="d-flex align-center pl-2">
              <v-row no-gutters>
                <v-col cols="5" class="d-flex align-center justify-left">Count</v-col>
                <v-col cols="7" no-gutters>
                  <v-row no-gutters>
                    <v-col cols="4">
                      <v-text-field dense outlined hide-details="auto" v-model="base[0]['Count']"></v-text-field>
                    </v-col>
                    <v-col cols="4" class="d-flex align-center justify-center">Color</v-col>
                    <v-col cols="4">
                      <v-text-field dense outlined hide-details="auto" v-model="base[0]['Color']"></v-text-field>
                    </v-col>
                  </v-row>
                </v-col>
              </v-row>
            </v-col>
            <v-col cols="2" class="d-flex align-center pl-2">
              <v-btn color="secondary">Info</v-btn>
            </v-col>
          </v-row>
        </v-tab-item>
        <v-tab-item :key="1" class="pl-5">
          <v-row no-gutters class="mt-5">
            <v-col cols="5" class="d-flex align-center">
              <v-row no-gutters>
                <v-col cols="5" class="d-flex align-left justify-left">Type</v-col>
                <v-col cols="7">
                  <v-text-field dense outlined hide-details="auto" v-model="detail[0]['Type']"></v-text-field>
                </v-col>
              </v-row>
            </v-col>
            <v-col cols="5" class="d-flex align-center pl-2">
              <v-row no-gutters>
                <v-col cols="5" class="d-flex align-center justify-left">Sub Type</v-col>
                <v-col cols="7">
                  <v-text-field dense outlined hide-details="auto" v-model="detail[0]['Sub Type']"></v-text-field>
                </v-col>
              </v-row>
            </v-col>
            <v-col cols="2" class="d-flex align-center pl-2"> </v-col>
          </v-row>
          <v-row no-gutters class="mt-5">
            <v-col cols="5" class="d-flex align-center">
              <v-row no-gutters>
                <v-col cols="5" class="d-flex align-center justify-left">Due TS</v-col>
                <v-col cols="7">
                  <v-text-field dense outlined hide-details="auto" v-model="detail[0]['Due TS']"></v-text-field>
                </v-col>
              </v-row>
            </v-col>
            <v-col cols="5" class="d-flex align-center pl-2">
              <v-row no-gutters>
                <v-col cols="5" class="d-flex align-center justify-left">Current Status</v-col>
                <v-col cols="7">
                  <v-text-field dense outlined hide-details="auto" v-model="detail[0]['Current Status']"></v-text-field>
                </v-col>
              </v-row>
            </v-col>
          </v-row>
          <v-row no-gutters class="mt-5">
            <v-col cols="5" class="d-flex align-center">
              <v-row no-gutters>
                <v-col cols="5" class="d-flex align-center justify-left">Bank ID</v-col>
                <v-col cols="7">
                  <v-text-field dense outlined hide-details="auto" v-model="detail[0]['Bank ID']"></v-text-field>
                </v-col>
              </v-row>
            </v-col>
            <!-- <v-col cols="5" class="d-flex align-center pl-2">
              <v-row no-gutters>
                <v-col cols="5" class="d-flex align-center justify-left">Count</v-col>
                <v-col cols="7" no-gutters>
                  <v-row no-gutters>
                    <v-col cols="4">
                      <v-text-field dense outlined hide-details="auto" v-model="detail[0]['Count']"></v-text-field>
                    </v-col>
                    <v-col cols="4" class="d-flex align-center justify-center">Color</v-col>
                    <v-col cols="4">
                      <v-text-field dense outlined hide-details="auto" v-model="detail[0]['Color']"></v-text-field>
                    </v-col>
                  </v-row>
                </v-col>
              </v-row>
            </v-col>
            <v-col cols="2" class="d-flex align-center pl-2">
              <v-btn color="secondary">Info</v-btn>
            </v-col> -->
          </v-row>
        </v-tab-item>
      </v-tabs-items>
    </v-card>
  </div>
</template>

<script>
import { tab, info, base, detail } from "../comment/data";

export default {
  data: () => ({
    tab: tab,
    info: info,
    base: base.map((item) => {
      let useData = {};
      item.data.forEach((data) => {
        useData[data.key] = data.value;
      });
      return useData;
    }),
    detail: detail.map((item) => {
      let useData = {};
      item.data.forEach((data) => {
        useData[data.key] = data.value;
      });
      return useData;
    }),
    selectTab: 0,
  }),
  created: () => {},
};
</script>
