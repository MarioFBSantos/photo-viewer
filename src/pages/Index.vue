<template>
  <q-page class="items-center">
    <div >

      <div class="alignBar q-pt-md">
        <div class="searchBar">
          <q-input borderless v-model="search" label="Search" class="q-px-sm"/>
        </div>
      </div>

      <grid :photos="filteredFiles" class="q-pa-md"/>
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
search = '';
photoList: photoInteface= {
      id: 0,
      author: '',
      width: 0,
      height: 0,
      url: '',
      download_url: '',
};
imageList = this.items;
fFiles: any;
get items(){
 		axios
			.get('https://picsum.photos/v2/list?page=5&limit=35')
			.then(response => {
				this.photoList = response.data;
			})
			.catch(error => console.log(error))

  return this.photoList;
}

get filteredFiles(){
  this.fFiles = this.photoList;
  if(this.search)  return this.fFiles.filter(({author}) => {
    return new RegExp(this.search, 'gi').test(author);
  });

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
  .alignBar{
    display:flex;
    justify-content: space-around;
  }
  .searchBar{
    border-radius: 8px;
    width: 70%;
    background-color: #fff;
  }
  .imageCard{
    // display: flex;
    overflow: hidden;
    display: -webkit-box;
  }

</style>
