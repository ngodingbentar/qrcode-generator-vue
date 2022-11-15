<template>
  <div class="qrcode">
    <h3>QRCode Generator</h3>
    <div class="container">
      <canvas class="canvas"></canvas>
    </div>
    <input placeholder="Enter your website or text here" id="qrInput" />
    <button @click="generateQR()">generate</button>
    <p v-if="isError">{{isError}}</p>
  </div>
</template>

<script setup>
import QRCode from 'qrcode'
import { ref } from 'vue'

const isError = ref(false)

const generateQR = () => {
      console.log('generateQR');
      const input = document.getElementById('qrInput');
      const canvas = document.querySelector('canvas');
      const url = input.value;
      QRCode.toCanvas(canvas, url, (error) => {
        if (error) {
          console.error(error);
          isError.value = error;
        }
        else isError.value = '';
      });
    }
</script>

<style>
    .qrcode {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    .qrcode .container {
      width: 200px;
      height: 200px;
      border: 2px solid black;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    input {
      width: 250px;
      margin: 20px;
    }
  </style>
