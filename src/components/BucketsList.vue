<template>
  <div></div>
</template>

<script>

import globleConfig from '../../globleConfig.json'
export default {
    data(){
        return {
            documentTree:[]
        }
    },
    created(){
        var Minio = require('minio')
var minioClient = new Minio.Client(globleConfig.minio);
        minioClient.listBuckets((error, buckets) => {
            if (error){
                console.log(error);
            }
            console.log(buckets);
        });
    }
}
</script>

<style>

</style>