<template>
  <div>
    <div class="nav">
      <h3>Ngodingbentar</h3>
    </div>
    <div class="qrcode">
      <h3>QRCode Generator</h3>
      <div class="container">
        <canvas class="canvas"></canvas>
      </div>
      <input placeholder="Enter your website or text here" id="qrInput" />
      <button @click="generateQR()" class="btn">Generate</button>
      <p v-if="isError">{{isError}}</p>
    </div>
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
  body {
    margin: 0px;
  }
  .nav {
    background: #0984e3;
    padding: 1px;
    color: white;
  }

  .nav h3 {
    margin-left: 20px;
  }
  .qrcode {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-weight: 700;
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
    padding: 10px;
    border-radius: 10px;
  }

  .btn {
    padding: 10px;
    background-color: #0984e3;
    color: white;
    border: none;
    border-radius: 10px;
  }
  </style>
