<template>
  <masonry
    :cols="3"
    :gutter="15"
    >
      <div v-for="(item, index) in photos" :key="item.id">
        <div>
          <img :src="item.download_url" class="photo"/>
          <div>
            <!-- <div>{{item.width,' x ', item.height}}</div> -->
            <div>{{item.author}}</div>

          </div>
        </div>
      </div>
  </masonry>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator';
import photoInteface from '../interface/photo';
import VueMasonry from 'vue-masonry-css'
Vue.use(VueMasonry);
@Component({
  components: {}

})
export default class grid extends Vue {

@Prop()
photos!: photoInteface;

}
</script>

<style lang="scss" scoped>
  .photo{
    width: 99%;
  }
</style>
