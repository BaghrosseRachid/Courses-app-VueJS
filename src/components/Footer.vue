<template lang="">
     
     <div class="card text-center mt-5">
            <div class="card-header">
                {{ text }}
            </div>
            <div class="card-body">
                <blockquote class="blockquote mb-0">
                <footer class="blockquote-footer">{{ title }} <a :href="url">{{ url }}</a> </footer>
                </blockquote>
            </div>
     </div>

</template>
<script>
export default {
    props: ['url', 'title', 'text']
}
</script>
<style lang="">
    
</style>