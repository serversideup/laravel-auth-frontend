<template>
    <div>
        {{ user }}
    </div>
</template>

<script>
export default {
    data(){
        return {
            user: {}
        }
    },

    middleware: 'auth',

    mounted(){
        this.loadUser();
    },

    methods: {
        loadUser(){
            this.$axios.$get('/api/v1/user')
                .then(function( response ){
                    this.user = response;
                }.bind(this));
        }
    }
}
</script>