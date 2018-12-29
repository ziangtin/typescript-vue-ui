<template>
    <div class="home">
        <switch-btn v-model="open" />
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import SwitchBtn from '@/components/button/switch_btn.vue'; // @ is an alias to /src

@Component({
  components: {
    SwitchBtn
  }
})
export default class Home extends Vue {
  private open: boolean = true;
}
</script>

<style lang="less" scoped>
@import '../style/animate';
</style>
