<template>
    <v-app>
    <v-app-bar
      app
      height="100"
      color="white"
      flat
    >
      <v-layout align-center>
        <v-flex>
          <v-text-field color="grey" v-model="frase" @keydown.enter="searchPhoto(frase)" placeholder="Search" class="mt-7" flat solo-inverted prepend-inner-icon="mdi-magnify"/>
        </v-flex>
          <v-btn height="45" class="mx-2 ml-4" color="white">
            <v-icon>
              mdi-tune-vertical
            </v-icon>
          </v-btn>
          <v-btn height="45" class="ml-2" dark @click="addPhoto()">
             <v-icon>
              mdi-plus
            </v-icon>
          </v-btn>
      </v-layout>
    </v-app-bar>

    <v-navigation-drawer app permanent>
      <v-list-item>
        <v-list-item-avatar>
          <v-img width="10" lazy-src="https://upload.wikimedia.org/wikipedia/commons/0/08/Pinterest-logo.png" src="https://upload.wikimedia.org/wikipedia/commons/0/08/Pinterest-logo.png" />
        </v-list-item-avatar>
        <v-list-item-content>
          <v-list-item-title class="title">
            <v-layout align-center>Pinterest</v-layout>
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <div class="mx-4 subtitle-2 grey--test">Insights</div>
      <v-list
        dense
        nav
      >
        <v-list-item 
          link
        >
          <v-list-item-icon>
            <v-icon>mdi-message-reply-text</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>Messages</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item 
          link
        >
          <v-list-item-icon>
            <v-icon>mdi-bell</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>Notifications</v-list-item-title>
          </v-list-item-content>
          <v-list-item-avatar size="25" color="orange" class="white--text subtitle-2">
            <v-flex text-center>2</v-flex>
          </v-list-item-avatar>
        </v-list-item>
      </v-list>
      <v-card flat>
        <v-img aspect-ratio="1" src="https://img.freepik.com/vector-gratis/ilustracion-vector-concepto-abstracto-equipo-devops-miembro-equipo-desarrollo-software-flujo-trabajo-agil-modelo-equipo-devops-trabajo-equipo-ti-gestion-proyectos-metafora-abstracta-practica-integrada_335657-2299.jpg?size=338&ext=jpg&ga=GA1.2.1646937597.1645539938"></v-img>
      </v-card>
      <v-layout class="pt-2 px-8">
        <v-flex text-center>
          <div class="subtitle-2 blue--text">
            Unlock Business Tools
          </div>
          <div class="caption">
            Hurry Up! Noew You can unlock our new business tools at your Convenience.
          </div>
        </v-flex>
      </v-layout>
      <v-layout align-center class="my-8 mx-4">
        <v-card style="border-radius:10px" class="mx-auto" elevation="2">
         <v-list-item>
           <v-list-item-avatar>
            <v-img src="https://images.unsplash.com/photo-1522075469751-3a6694fb2f61?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1160&q=80" />
           </v-list-item-avatar>
         <v-list-item-content>
           <v-list-item-title class="subtitle-2">John Nieves</v-list-item-title>
           <v-list-item-subtitle>Content Creator</v-list-item-subtitle>
         </v-list-item-content>
         <v-list-item-action>
           <v-icon>mdi-chevron-right</v-icon>
         </v-list-item-action>
         </v-list-item>
        </v-card>
      </v-layout>
    </v-navigation-drawer>

    <v-main>
        <home-page :photos="photoList" />
    </v-main>
  </v-app>
</template> 

<script>
import HomePage from '@/pages/HomePage.vue'
export default {
    components:{
        HomePage
    },
    data(){
        return {
            items: [
                { title: 'Home', icon: 'mdi-home-variant' },
                { title: 'Recent', icon: 'mdi-clock-time-three' },
                { title: 'Following', icon: 'mdi-account-group' },
            ],
            items2: [
                { title: 'Messages', icon: 'mdi-view-dashboard' },
                { title: 'Notifications', icon: 'mdi-image' },
            ],
            right: null,
            photoList:[],
            frase:""
        }
    },
    methods:{
      addPhoto(){
          const client_id='cbcBYvdmB1c5zywV-8hWMJXMlsqbiR1V_3_TAnH_pzM';
          fetch('https://api.unsplash.com/photos/random?client_id='+ client_id)
          .then(response => response.json())
          .then(data => (this.photoList.push(data)));
      },
      searchPhoto(frase){
        if(frase){
          const client_id='cbcBYvdmB1c5zywV-8hWMJXMlsqbiR1V_3_TAnH_pzM';
          fetch('https://api.unsplash.com/photos/random?query='+frase+'&count=10&client_id='+ client_id)
          .then(response => response.json())
          .then(data => (this.photoList = data));
        }
      }
    },
    watch: {
    frases: function (newQuestion, oldQuestion) {
      if(newQuestion){
        this.searchPhoto(newQuestion)
      }
    }
  },
    created(){
        const client_id='cbcBYvdmB1c5zywV-8hWMJXMlsqbiR1V_3_TAnH_pzM';
        fetch('https://api.unsplash.com/photos/random?count=10&client_id='+ client_id)
        .then(response => response.json())
        .then(data => (this.photoList = data));
    }
}
</script>

