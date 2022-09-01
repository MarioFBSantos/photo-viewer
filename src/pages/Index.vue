<template>
  <q-page class="items-center">
    <div >
      <div class="alignBar q-pt-md">
        <div class="searchBar">
          <q-input borderless v-model="search" label="Search" class="q-px-sm"/>
        </div>
      </div>
      <grid :photos="filteredFiles" class="q-pa-md"/>
      <div class="buttonsContainer">
        <q-btn label="Previous page" @click="Page(-1)" class="bg-white" text-color="black" :disable="page === 1"></q-btn>
        <q-btn label="Next page" @click="Page(+1)" class="bg-white" text-color="black"></q-btn>
      </div>
    </div>
  </q-page>
</template>

<script lang="ts">
import { Vue, Component, Watch } from 'vue-property-decorator';
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
fFiles: photoInteface | any = this.photoList;
page: number = 1;
timer:any = 0;
@Watch('limit')
onLimitChange(){
  this.photoList =  this.items;
}

    get items(){
    const url = `https://picsum.photos/v2/list?page=${this.page}&limit=15`
      this.$axios
          .get(url)
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

    Page(orientation: number){
        this.page = this.page + orientation;
      this.showLoading();
      document.body.scrollTop = 0;
      document.documentElement.scrollTop = 0;
      this.items;
    }

    showLoading () {
      this.$q.loading.show()
      this.timer = setTimeout(() => {
        this.$q.loading.hide()
        this.timer = void 0
      }, 1000)
    }

    mounted(){
      this.page = 1;
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
  .buttonsContainer{
    display: flex;
        justify-content: center;
        gap: 3px;
  }

</style>
