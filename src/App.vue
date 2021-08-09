<template>
<div class="d-flex flex-column flex-md-row align-items-center p-3 px-md-4 mb-3 bg-white border-bottom shadow-sm">
        <h5 class="my-0 mr-md-auto font-weight-normal">
          <img
            src="https://dadan.io/wp-content/uploads/2020/11/dadan.svg"
            alt=""
            height="32"
          />
        </h5>
        <nav class="my-2 my-md-0 mr-md-3"></nav>
      </div>
      <div class="container">
        <div class="row">
          <div class="col-md-2 mb-3">
            <RecordVideoButton title = "Select Video" 
            v-bind:showSvg="true"
            v-bind:showPreview="true"
            v-bind:copyToClipboard="true"
            buttonClass=""
            buttonStyle=""
            type="select"
            @onFailure="handleResponse"
            @onSuccess="handleResponse"/>
          </div>
        </div>
        <div class="row">
          <div v-if="videos.length > 0" class="col-md-12">
            <ul class="list-group">
              <li class="list-group-item" v-for="(video , index) in videos" v-bind:key="index">
                <div>
                  <code>title : {{video.title}}</code>
                </div>
                <div>
                  <code>thumbnailUrl : {{video.thumbnailUrl}}</code>
                </div>
                <div>
                  <code>sharedUrl : {{video.sharedUrl}}</code>
                </div>
                 <div>
                  <code>embedUrl : {{video.embedUrl}}</code>
                </div>
                  <div>
                  <code>customHtmlFormat : {{video.customHtmlFormat}}</code>
                </div>
                <div>
                  <code>
                        =============================================================================================================
                  </code>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
      </template>
<script>
import RecordVideoButton from 'vue-dadan-sdk';
export default {
  name : "App",
  data : function(){
    return{
      videos : []
    }
  },
  components : {
    RecordVideoButton
  },
  methods : {
    handleResponse : function({success, data, message}) {
      if (success) {
        if (data) {
          this.videos = data;
          }
        } else {
          this.videos = [];
          console.log(message);
        }
    }
  }
}
</script>