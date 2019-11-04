<template>
  <div>
    <div class="header">
          <i class="fa fa-bars" @click="toggleSettings"></i>
      <div class="setting-wrapper">
          <div class="setting-container" v-bind:class="{disable: openSetting}">
            <span>종료시간</span>
            <input type="text" v-model="date">
          </div>
      </div>
    </div>
    <div class="hello">
      <div>
        <image-uploader
        :debug="1"
        :maxWidth="300"
        :autoRotate=true
        outputFormat="verbose"
        :preview=true
        :className="['fileinput', { 'fileinput--loaded' : hasImage }]"
        capture="environment"
        doNotResize="['gif', 'svg']"
        @input="setImage"
      >
            <label for="fileInput" slot="upload-label" v-bind:class="{disable: hasImage}">
              <figure>
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="32"
                  height="32"
                  viewBox="0 0 32 32"
                >
                  <path
                    class="path1"
                    d="M9.5 19c0 3.59 2.91 6.5 6.5 6.5s6.5-2.91 6.5-6.5-2.91-6.5-6.5-6.5-6.5 2.91-6.5 6.5zM30 8h-7c-0.5-2-1-4-3-4h-8c-2 0-2.5 2-3 4h-7c-1.1 0-2 0.9-2 2v18c0 1.1 0.9 2 2 2h28c1.1 0 2-0.9 2-2v-18c0-1.1-0.9-2-2-2zM16 27.875c-4.902 0-8.875-3.973-8.875-8.875s3.973-8.875 8.875-8.875c4.902 0 8.875 3.973 8.875 8.875s-3.973 8.875-8.875 8.875zM30 14h-4v-2h4v2z"
                  ></path>
                </svg>
              </figure>
              <span class="upload-caption">{{
                hasImage ? "Replace" : "Click to upload"
              }}</span>
            </label>
        </image-uploader>

      </div>
      <div class="countdown">
        <div class="block">
          <p class="digit">{{ days | two_digits }}</p>
          <p class="text">Days</p>
        </div>
        <div class="block">
          <p class="digit">{{ hours | two_digits }}</p>
          <p class="text">Hours</p>
        </div>
        <div class="block">
          <p class="digit">{{ minutes | two_digits }}</p>
          <p class="text">Minutes</p>
        </div>
        <div class="block">
          <p class="digit">{{ seconds | two_digits }}</p>
          <p class="text">Seconds</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  mounted () {
    window.setInterval(() => {
      this.now = Math.trunc((new Date()).getTime() / 1000)
    }, 1000)
  },
  data () {
    return {
      now: Math.trunc((new Date()).getTime() / 1000),
      date: new Date(),
      hasImage: false,
      openSetting: false,
      image: null
    }
  },
  methods: {
    setImage: function (output) {
      this.hasImage = true
      this.image = output
    },
    toggleSettings: function () {
      this.openSetting = !this.openSetting
    }
  },
  computed: {
    dateInMilliseconds () {
      return Math.trunc(Date.parse(this.date) / 1000)
    },
    seconds () {
      return (this.dateInMilliseconds - this.now) % 60
    },
    minutes () {
      return Math.trunc((this.dateInMilliseconds - this.now) / 60) % 60
    },
    hours () {
      return Math.trunc((this.dateInMilliseconds - this.now) / 60 / 60) % 24
    },
    days () {
      return Math.trunc((this.dateInMilliseconds - this.now) / 60 / 60 / 24)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
@import url(https://fonts.googleapis.com/css?family=Roboto+Condensed:400|Roboto:100);

.hello {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
#app {
    align-items: center;
    bottom: 0;
    background-color: #ffffff;
    display: flex;
    justify-content: center;
    left: 0;
    position: absolute;
    right: 0;
    top:0;
}

.countdown {
  display: inline-flex;
}

.block {
    display: flex;
    flex-direction: column;
    margin: 20px;
}

.text {
    color: #1abc9c;
    font-size: 25px;
    font-family: 'Roboto Condensed', serif;
    font-weight: 40;
    margin-top:10px;
    margin-bottom: 10px;
    text-align: center;
}

.digit {
    color: #ecf0f1;
    font-size: 130px;
    font-weight: 100;
    font-family: 'Roboto', serif;
    margin: 10px;
    text-align: center;
}

.disable {
  display: none !important;
}
#fileInput {
  display: none;
}

.header {
  position: absolute;
  padding: 20px;
  top: 0;
  right: 0;
}

.setting-wrapper {
  position: absolute;
  right: 0;
  width: 500px;
  background-color: azure;
}

.setting-container {
  display: flex;
}

</style>
