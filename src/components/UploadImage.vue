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

      const formData = new FormData();
      formData.append('file', this.file); 
      axios.post('https://t57wg2rlb3.execute-api.us-east-1.amazonaws.com/prod/api/upload', formData, {
        headers: {
                'Content-Type': 'application/json'
            }
      })
      .then(response => {
        console.log('File uploaded successfully:', response.data);
     
      })
      .catch(error => {
        console.error('Error uploading file:', error);
       
      });
    }
  }
};
</script>
