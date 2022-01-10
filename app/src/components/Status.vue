<script lang="ts">
import { defineComponent, ref } from "vue"
import axios from 'axios'

interface StatusResponse {
  status: string
}

export default defineComponent({
  setup() {
    const status = ref<string>('Loading...')

    const getStatus = async () => {
      const response = await axios.get<StatusResponse>('/api/status')
      status.value = response.data.status
    }
    getStatus()

    return {
      status
    }
  }
})
</script>

<template>
  <div class="status-frame">
    <div class="status-key">status</div>
    <div class="status-value">{{ status }}</div>
  </div>
</template>

<style scoped>
.status-frame {
  margin: 40px auto;
  border: solid 3px #210091;
  background-color: #eee;
  display: block;
  width: 200px;
  padding: 12px 10px;
  font-family: monospace;
  font-size: xx-large;
  border-radius: 16px;
  width: 340px;
}
.status-key {
  margin: 0.5em auto 0.5em;
  color: #210091;
}
.status-value {
  margin: 0.5em auto 0.5em;
  font-weight: bolder;
  color: black;
}
</style>