<template>
    <div>
        <h2>Homework Component</h2>
   
        <div class="container my-4">
            <div class="row">
                <div class="col-4 my-3" v-for="(datas,i) in info" :key="i">
                    <div class="card">
                        <img :src="datas.item_photo" class="card-img-top">
                        <div class="card-body">
                            <h5 class="card-title">{{datas.item_name}}</h5>
                            <p class="card-text" v-html="datas.description"></p>
                            <p class="card-text">{{datas.price}}MMK</p>
                            <a href="#" class="btn btn-primary">Detail</a>
                            <button class="btn btn-primary ml-5">Add To Cart</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script type="text/javascript">
export default {
    name: 'Home',
    data() {
        return {
            loading: true,
            error: false,
            info: null
        }
    },
    mounted() {
        this.getdatas();
    },
    methods: {
        getdatas() {
            this.$http.get('http://jetpackmall.aungchanoo.me/api/items')
                .then(res => {
                    console.log(res);
                    this.info = res.data.data
                })
                .catch(err => {
                    this.error = true;
                    console.log(err);
                })
                .finally(() => {
                    this.loading = false;
                })
        }
    }
};
</script>
<style type="text/css">
.card-img-top {
    width: 100%;
    height: 250px;
    object-fit: cover;
}
</style>