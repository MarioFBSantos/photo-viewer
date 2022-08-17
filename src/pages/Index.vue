<template>
  <q-page class="items-center">
    <div >
      <!-- <div>{{photoList}}</div> -->
      <grid :photos="photoList" class="q-pa-md"/>
      </div>
    </div>
  </q-page>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';
import axios from 'axios';
import photoInteface from './interface/photo'
import grid from './grid/grid.vue'
@Component({
  components: {
    grid
    }

})
export default class PageIndex extends Vue {

photoList: photoInteface= {
      id: 0,
      author: '',
      width: 0,
      height: 0,
      url: '',
      download_url: '',
};
imageList = this.items;

get items(){
 		axios
			.get('https://picsum.photos/v2/list?page=5&limit=35')
			.then(response => {
				this.photoList = response.data;
			})
			.catch(error => console.log(error))

  return this.photoList;
}

mounted(){
  this.photoList =  this.items;
}
}
</script>

<style lang="scss" scoped>
  html{
    background-color: #666;
  }
  .imageCard{
    // display: flex;
    overflow: hidden;
    display: -webkit-box;
  }

</style>
