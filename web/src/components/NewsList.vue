<template>
    <div>
        <ul class="news-list-items" v-if="items !== undefined">
            <li class="news-list-item" v-for="(item, index) in items" :key="index">
                <el-card shadow="hover">
                    <router-link :to="`/news/${item.news_path}`">
                        <!--<div class = "item-mask"></div>-->
                        <img :src="item.cover_img" alt="">
                        <div class="item-content">
                            <h2>{{ item.news_title }}</h2>
                            <p>{{ item.news_desc }}</p>
                            <span>{{ item.publish_time }}</span>
                        </div>
                    </router-link>
                </el-card>
            </li>
        </ul>
        <span class="is-null" v-else>暂无数据</span>
    </div>
</template>
<script lang="ts" setup>
import { PropType, ref } from 'vue'
import mainStore from '@/store'

const props = defineProps({
  items: {
    type: Array as PropType<Array<any>>,
    default: () => ([])
  }
})

const currentPage = ref(1)

function setArticlePath (path: string) {
  // console.log("path====>",path);
  mainStore.commit('SET_ARTICLE_PATH', {
    path: path
  })
}
</script>
<style lang="less" scoped>
.news-list-item {
    padding: 0 15px 15px 8px;
    position: relative;
    border-radius: 8px;

    img {
        width: 198px;
        height: 125px;
        border-style: none;
    }

    a {
        color: rgba(0, 0, 0, 1);
        transition: color .3s;
        overflow: hidden;
        display: flex;
        cursor: pointer;
    }

    a:hover {
        color: var(--hover_color);
    }
}

.el-card {
    border: none;
    transition: .5s;
}

.is-null {
    display: flex;
    justify-content: center;
    margin-top: 45px;
    color: #777
}

.item-mask {
    display: block;
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0);
    transition: all .3s;
    border-radius: 8px;
}

.item-content {
    margin-left: 40px;
    width: calc(100% - 238px);

    h2 {
        font-size: 20px;
        font-weight: 500;
        overflow: hidden;
        //white-space: nowrap;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 2;
    }

    p {
        margin: 10px 0;
        font-size: 15px;
        color: #777;
        letter-spacing: 0;
        line-height: 22px;
        overflow: hidden;
        //white-space: nowrap;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 1;
    }

    span {
        color: #b8b8b8;
        line-height: 14px;
    }
}
</style>
