<template>
  <v-card flat>
      <v-img style="border-radius:16px" :src="meta.urls.regular"></v-img>
      <v-layout align-center class="px-3 pt-3 pb-2">
          <v-avatar size="36" color="white">
              <v-img :src="meta.user.profile_image.small"></v-img>
          </v-avatar>
          <v-flex class="ml-3">
            <div class="subtitle-2">{{meta.user.name}}</div>
            <div class="body-1 grey--text text--darken-1">{{meta.user.username}}</div>
          </v-flex>
      </v-layout>
  </v-card>
</template>

<script>
export default {
    props:{
        meta:{
            type: Object,
            default: function(){
                return {};
            }
        }
    }
}
</script>

<style>

</style>