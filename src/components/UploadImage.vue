<template>
  <div>
    <h1>Upload Image</h1>
    <input type="file" @change="onFileChange" />
    <button :disabled="!file" @click="uploadFile">Upload</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'UploadImage',
  data() {
    return {
      file: null
    };
  },
  methods: {
    onFileChange(e) {
      this.file = e.target.files[0];
    },
    uploadFile() {
      if (!this.file) return;

      convertImageToBase64(this.file, function(base64String) {
        axios.post('your-api-endpoint', {
            image: base64String  
        }, {
            headers: {
                'Content-Type': 'application/json'
            }
        })
        .then(response => {
            console.log('Upload successful:', response.data);
        })
        .catch(error => {
            console.error('Upload failed:', error);
        });
    });

    }
  }
};

function convertImageToBase64(file, callback) {
    const reader = new FileReader();
    reader.onload = function(e) {
        const base64String = e.target.result.split(',')[1];
        callback(base64String);
    };
    reader.readAsDataURL(file);
}

</script>
