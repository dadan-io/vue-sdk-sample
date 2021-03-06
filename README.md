# Vue Dadan SDK Sample

A lightweight Vue app that shows how to use [vue-dadan-sdk](https://www.npmjs.com/package/vue-dadan-sdk) package , which used for checking, validating, and manipulating [Google Dadan Extension](https://haal.link.sa/onboarding/download) with Vue.

## Install

```bash
npm install
```

## Usage

In App.vue file we import the RecordVideoButton component

```vue
<script>
import RecordVideoButton from "vue-dadan-sdk"; //Main component to import
export default {
  name: "App",
  data: function() {
    return {
      videos: [], //initial state used to get recorded or selected videos
    };
  },
  components: {
    RecordVideoButton, //our component
  },
  methods: {
    handleResponse: function({ success, data, message }) {
      if (success) {
        if (data) {
          this.videos = data;
        }
      } else {
        this.videos = [];
        console.log(message);
      }
    },
  },
};
</script>
```

In App.vue file template we add the component with props

```vue
<template>
  <RecordVideoButton
    title="Select Video"
    v-bind:showSvg="true"
    v-bind:showPreview="true"
    v-bind:copyToClipboard="true"
    buttonClass=""
    buttonStyle=""
    type="select"
    @onFailure="handleResponse"
    @onSuccess="handleResponse"
  />
</template>
```

the handleResponse function in Methods , is a callback function which accept object with three parameters

```javascript
handleResponse : function({ success, data, message }) {
  if (success) {
    // only false when user close extension
    if (data) {
      // represnts the selected videos , or recorded video object after stop recording
      this.videos = data;
    }
  } else {
    this.videos = [];
    console.error(message); //User Closed Extension
  }
}
```

## Record Button Props

| Parameter         | Type      | Description                                                                                 |
| :---------------- | :-------- | :------------------------------------------------------------------------------------------ |
| `type`            | `string`  | **Required**. either record or select , else will show error                                |
| `title`           | `string`  | **Optional**. button title                                                                  |
| `buttonClass`     | `string`  | **Optional**. the default class , or your custom class                                      |
| `buttonStyle`     | `string`  | **Optional**. the default style , or your custom style as string                            |
| `showSvg`         | `boolean` | **Optional**. to show Svg icon in button                                                    |
| `showPreview`     | `boolean` | **Optional**. to show preview dialog of recorded video                                      |
| `copyToClipboard` | `boolean` | **Optional**. to notify user that video shared url was copied to clipboard as toast message |

## License

[MIT](https://choosealicense.com/licenses/mit/)
