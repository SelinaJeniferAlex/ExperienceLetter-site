<template>
  <div id="q-app" style="min-height: 100vh;">
    <div>
      <q-layout view="hHh Lpr lff" container style="height: 100vh">
        <q-drawer
          v-model="drawer"
          show-if-above

          :mini="!drawer || miniState"
          @click.capture="drawerClick"

          :width="300"
          :breakpoint="768"
          bordered
          
          :class="$q.dark.isActive ? 'bg-indigo-13' : 'bg-indigo-14'"
        >
          <q-scroll-area class="fit" :horizontal-thumb-style="{ opacity: 0 }">
            <q-list padding>
              <br>
              <q-item class="q-ma-md text-white" clickable v-ripple>
                <q-item-section avatar class="self-start text-h5 text-weight-bold" :class="{ 'iconHide': !miniState }">
                  <q-icon name="C"></q-icon>
                </q-item-section>

                <q-item-section class="text-h5 text-center text-weight-bold">
                  Company Name
                </q-item-section>
              </q-item>
              <br>
              <br>
              <q-item clickable v-ripple :class="{ 'active': activeItem === 'AddEmployeeData' }" @click="activateItem('AddEmployeeData')">
                <q-item-section class="text-white" avatar>
                  <q-icon name="account_box"></q-icon>
                </q-item-section>

                <q-item-section class="text-grey-4 text-h6">
                  Generate Service Letter
                </q-item-section>
              </q-item>
              <!-- <br> -->
              <!-- <q-item clickable v-ripple :class="{ 'active': activeItem === 'ViewEmployeeData' }" @click="activateItem('ViewEmployeeData')">
                <q-item-section class="text-white" avatar>
                  <q-icon name="equalizer"></q-icon>
                </q-item-section>

                <q-item-section class="text-grey-4 text-h6">
                  ViewEmployeeData
                </q-item-section>
              </q-item> -->
              <!-- <br> -->
              <q-item class="text-white" clickable v-ripple :class="{ 'active': activeItem === 'GenerateLetter' }" @click="activateItem('GenerateLetter')">
                <q-item-section avatar>
                  <q-icon name="note"></q-icon>
                </q-item-section>

                <q-item-section class="text-grey-4 text-h6">
                  Letter Template
                </q-item-section>
              </q-item>
              <br>
              <!-- <q-item class="text-white" clickable v-ripple :class="{ 'active': activeItem === 'SendEmail' }" @click="activateItem('SendEmail')">
                <q-item-section avatar>
                  <q-icon name="mail"></q-icon>
                </q-item-section>

                <q-item-section class="text-grey-4 text-h6">
                  SendEmail
                </q-item-section>
              </q-item> -->
            </q-list>
          </q-scroll-area>

          <!--
            in this case, we use a button (can be anything)
            so that user can switch back
            to mini-mode
          -->
          <div class="q-mini-drawer absolute" style="top: 50px; right: -19px">
            <q-btn
              dense
              round
              unelevated
              class="text-blue"
              color="white"
              :icon="miniState ? 'chevron_right' : 'chevron_left'"
              @click="toggleMiniState"
            ></q-btn> 
          </div>
        </q-drawer>
        <div class="lt-md">
          <div class="row q-pa-md bg-blue justify-center items-center">
            <div class="col-4 text-h5 text-weight-bold text-center text-blue-grey-9">Company Name</div>
          </div>
        </div>

        <q-page-container>
          <router-view />
        </q-page-container>
      </q-layout>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue'

export default {
  data() {
    return{
      drawer: false,
      miniState: false,
      activeItem: 'AddEmployeeData'
    }
  },
  methods: {
    toggleMiniState() {
      this.miniState = !this.miniState
    },
    drawerClick(e) {
      if (this.miniState) {
        this.miniState = false
        e.stopPropagation()
      }
    },
    activateItem(item) {
    this.activeItem = item;
    if (this.activeItem === 'SendEmail') {
      console.log("SendEmail");
      // Assuming `$router` is available, otherwise, you need to pass it as an argument or use inject
      this.$router.push({ path: '/SendEmail' });
    }
    else if (this.activeItem === 'ViewEmployeeData') {
      console.log("ViewEmployeeData");
      this.$router.push({ path: '/ViewEmployeeData' });
    }
    else if (this.activeItem === 'GenerateLetter') {
      console.log("GenerateLetter");
      this.$router.push({ path: '/GenerateLetter' });
    }
    else if (this.activeItem === 'AddEmployeeData') {
      console.log("AddEmployeeData");
      this.$router.push({ path: '/' });
    }
    }
  }, 
  computed: {
    miniDrawerIcon(){
      return miniState.value ? 'chevron_right' : 'chevron_left'
    }
  }
}
</script>

<style>
*{
  /* color: white; */
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
 }
.iconHide {
  display: none;
}
</style>
