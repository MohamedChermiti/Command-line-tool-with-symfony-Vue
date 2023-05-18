<template>
    <div>
      <h2>Payment Dates for the Year {{ getCurrentYear() }}</h2>
      <button class="btn btn-primary" @click="generatePaymentDates">Generate Payment Dates</button>
      <div v-if="showPopup" :class="[popupClass, 'popup']">
        {{ popupMessage }}
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        showPopup: false,
        popupClass: '',
        popupMessage: '',
      };
    },
    methods: {
      getCurrentYear() {
        return new Date().getFullYear();
      },
      generatePaymentDates() {
        fetch('/generate-payment-dates') // Update the URL to match your route path
          .then((response) => {
            if (response.ok) {
              return response.blob();
            } else {
              throw new Error('An error occurred while generating payment dates.');
            }
          })
          .then((blob) => {
            this.showPopup('Payment dates generated successfully.', 'success');
  
            const downloadUrl = URL.createObjectURL(blob);
            const link = document.createElement('a');
            link.href = downloadUrl;
            link.download = 'payment_dates.csv';
            link.style.display = 'none';
  
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
          })
          .catch((error) => {
            this.showPopup(error.message, 'fail');
          });
      },
      showPopup(message, status) {
        this.showPopup = true;
        this.popupClass = status;
        this.popupMessage = message;
  
        setTimeout(() => {
          this.showPopup = false;
          this.popupClass = '';
          this.popupMessage = '';
        }, 3000);
      },
    },
  };
  </script>
  
  <style>
  .popup {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #f1f1f1;
    border: 1px solid #ddd;
    padding: 20px;
    z-index: 9999;
  }
  
  .success {
    color: green;
  }
  
  .fail {
    color: red;
  }
  </style>
  