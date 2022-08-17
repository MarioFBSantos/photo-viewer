<template>
  <masonry
    :cols="3"
    :gutter="15"
    >
      <div v-for="(item, index) in photos" :key="item.id">
        <div class="frame q-mb-md">
          <img :src="item.download_url" class="photo"/>
          <div>
            <div class="author q-pl-xs q-pb-xs">{{item.author}}</div>
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
@font-face {
  font-family: inter;
  src: url('https://fonts.googleapis.com/css2?family=Inter&display=swap');
}
  .photo{
    width: 100%;
  }
  .author{
      position: inherit;
  }
  .frame{
    border-radius: 3px;
    background-color: #fff;
    color: #000;
    font-family: inter;
  }
</style>
