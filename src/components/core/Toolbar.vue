<template>
  <v-toolbar
    app
    flat
  >
    <v-toolbar-side-icon
      class="hidden-md-and-up"
      @click="toggleDrawer"
    />
    <v-container
      mx-auto
      py-0
    >
      <v-layout>
        <v-img
          :src="require('@/assets/logo.png')"
          class="mr-5"
          contain
          height="48"
          width="48"
          max-width="48"
          @click="$vuetify.goTo(0)"
        />
        <v-btn
          v-for="(link, i) in links"
          :key="i"
          :to="link.to"
          class="ml-0 hidden-sm-and-down"
          flat
          @click="onClick($event, link)"
        >
          {{ link.text }}
        </v-btn>
        <v-spacer />
        <v-text-field
          append-icon="mdi-magnify"
          flat
          hide-details
          solo-inverted
          style="max-width: 300px;"
        />
      </v-layout>
    </v-container>
  </v-toolbar>
</template>

<script>
  // Utilities
  import {
    mapGetters,
    mapMutations
  } from 'vuex'


  export default {
    computed: {
        // another way #1 to do it, parse the return info from store.js
        //...mapGetters(["links"])
        links() {
            // another way #2 to do it. also return from store.js
            //var results = this.$store.getters.links;
            var results = [
                {text:"Home",to:"/", href:"#home"},
                {text:"About",to:"/", href:"#about"},
                {text:"Travel",to:"/category/Travel"},
                {text:"Leisure",to:"/category/Leisure"},
                {text:"Political",to:"/category/Political"},
                {text:"Cooking",to:"/category/Cooking"},
                ]
            return results
        }
    },

    mounted() {
        console.log("drawer",this.$store.state.toggleDrawer);
        console.log("state",this.$store.state);
    },

    methods: {
      toggleDrawer () {
        console.log("toggle");
        this.$store.state.drawer = !this.$store.state.drawer;
        console.log(this.$store.state.drawer);
      },
      // alternative way to do in store.js, mutation function
      //...mapMutations(['toggleDrawer']),

      onClick (e, item) {
        e.stopPropagation()

        console.log("item",item);
        //if (item.to || !item.href) return

        if (item.href) this.$vuetify.goTo(item.href)
      }
    }
  }
  console.log(this);
</script>
