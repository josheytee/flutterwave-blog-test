<template>
    <main>
        <loader v-if="loading" />
        <div class="post" v-if="post">
            <div class="post__top">
                <span>By Ryan Jackson</span>
                <span>{{ post.date }} </span>
            </div>
            <h2 class="post__title" v-html="post.title.rendered"></h2>
            <div class="post__body" v-html="post.content.rendered"></div>
        </div>
    </main>
</template>

<script>
import Loader from "@/components/Loader.vue";
export default {
    data() {
        return {
            post: null,
            loading: false
        }
    },
    components: { Loader },
    methods: {
        getPostById(id) {
            this.loading = true;
            const api = 'https://techcrunch.com/wp-json/wp/v2/posts/' + id
            this.axios.get(api).then((response) => {
                this.post = response.data
                // console.log(response.data)
                this.loading = false;
            })

        }
    },
    mounted() {
        const id = this.$route.params.postId;
        console.log(id, "here")
        this.getPostById(id);
    }
}
</script>

<style lang="scss">
.post {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    margin-top: 2rem;
    font-family: 'SF Pro Text';
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 21px;
    /* or 150% */


    /* --c-black-20 */


    &__top {
        display: flex;
        gap: 10px;
    }

    &__title {
        font-size: 24px;
        font-weight: 700;
        line-height: 1.3;
        margin-bottom: 1rem;
    }

    &__body {
        color: #6E6E6E;

    }
}
</style>