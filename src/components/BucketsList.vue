<template>
  <v-treeview
    v-model="tree"
    :items="documentTree"
    :open="open"
    activatable
    item-key="name"
    open-on-click
  >
    <template v-slot:prepend="{ item, open }">
      <v-icon v-if="!item.file">
        {{ open ? 'mdi-folder-open' : 'mdi-folder' }}
      </v-icon>
      <v-icon v-else>
        {{ files[item.file] }}
      </v-icon>
    </template>
  </v-treeview>
</template>

<script>
import globleConfig from '../../globleConfig.json'
export default {
    data(){
        return {
            documentTree:[],
            tree:[],
            open:[],
            files: {
                html: 'mdi-language-html5',
                js: 'mdi-nodejs',
                json: 'mdi-code-json',
                md: 'mdi-language-markdown',
                pdf: 'mdi-file-pdf',
                png: 'mdi-file-image',
                txt: 'mdi-file-document-outline',
                xls: 'mdi-file-excel',
            },
        }
    },
    created(){
        var Minio = require('minio')
        var minioClient = new Minio.Client(globleConfig.minio);
        let _this = this;
        minioClient.listBuckets((error, buckets) => {
            if (error){
                _this.$notify({
                    type:'error',
                    message:'连接Minio服务器失败！'
                })
            }
            buckets.forEach(bucket => {
                bucket.children = [];
                let stream = minioClient.listObjects(bucket.name,'',false)
                stream.on('data',(obj) => {
                    console.log(obj);
                });
                stream.on('error',error => console.log(error));
                _this.documentTree.push(bucket)
            });
        });
    }
}
</script>

<style>

</style>