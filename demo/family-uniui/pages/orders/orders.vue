<template>
  <view class="container">
    <view class="uni-padding-wrap uni-common-mt">
      <uni-segmented-control
        :current="current"
        :values="items"
        style-type="text"
        :active-color="activeColor"
        @clickItem="onClickItem"
      />
    </view>
    <view class="content">
      <view v-if="current === 0" class="order">
        <img src="/static/public/empty.png" class="img" v-if="!list.length" />
      </view>
      <view v-if="current === 1" class="order">
        <img src="/static/public/empty.png" class="img" v-if="!list.length" />
      </view>
      <view v-if="current === 2" class="order">
        <img src="/static/public/empty.png" class="img" v-if="!list.length" />
      </view>
      <view v-if="current === 3" class="order">
        <img src="/static/public/empty.png" class="img" v-if="!list.length" />
      </view>
      <view v-if="current === 4" class="order">
        <img src="/static/public/empty.png" class="img" v-if="!list.length" />
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref } from "vue";
import { onLoad } from "@dcloudio/uni-app";
import api from "../../api/api";

const current = ref(0);
const items = ref(["全部", "待支付", "已取消", "已支付", "已退款"]);
const activeColor = ref("#1BBCB6");
const list = ref([]);

function onClickItem(e) {
  // 具体搜索请自行实现
  if (current.value !== e.currentIndex) {
    current.value = e.currentIndex;
  }
}

async function init(opId) {
  if (opId === 2) {
    const res = await api.order.cf_order();
    if (res?.data.data) {
      list.value = res.data.data;
    }
  } else {
    const res = await api.order.wz_order();
    if (res?.data.data) {
      list.value = res.data.data;
    }
  }
}

onLoad((e) => {
  init(e.op_id);
});
</script>

<style lang="scss">
.container {
  .content {
    .order {
      position: relative;
      .img {
        position: absolute;
        bottom: -700rpx;
        left: 250rpx;
        width: 370rpx;
        height: 310rpx;
      }
    }
  }
}
</style>
