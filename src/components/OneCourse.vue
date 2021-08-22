<template lang="">
    <div class="card my-3">
        <img class="card-img-top" :src="course.image" :alt="course.title">
            <div class="card-body">
                <h4 class="card-title">{{ course.title }}</h4>
                    <p class="card-text"> The more you Learn the more you earn <i class="fa fa-edge" aria-hidden="true"></i> </p>
                    <button class="btn btn-sm btn-danger" @click="deleteOne(course.id)">Supprimer</button>
                    <button class="btn btn-sm btn-dark ml-2">{{course.category}}</button>
                   
                    <div class="my-3">
                        <span class="badge badge-pill badge-primary ml-2" v-for="tag in course.tags">{{ tag }}</span>
                    </div>
            </div>
        </div>
</template>
<script>
export default {
    props: ['course'],
    methods: {
        deleteOne(id) {
            this.$emit('delete', id)
        }
    }
}
</script>
<style lang="">
    
</style>