<template>
    <div id="login">
        <div class="w-1/2 mx-auto">
            <div class="w-full flex flex-col mt-2">
                <label>Email</label>
                <input type="text" class="rounded border-gray-300 border p-2" v-model="email"/>
            </div>
            <div class="w-full flex flex-col mt-2">
                <label>Password</label>
                <input type="password" class="rounded border-gray-300 border p-2" v-model="password"/>
            </div>
            <div class="w-full flex flex-col mt-2">
                <button class="rounded text-white bg-blue-500 cursor-pointer px-5 py-2" v-on:click="login()">Login</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            email: '',
            password: '',
        }
    },

    methods: {
        login(){
            this.$auth.loginWith( 'laravelSanctum', {
                data: {
                    email: this.email,
                    password: this.password
                }
            }).then(function( response ){
                this.$router.push({
                    path: '/user'
                });
            }.bind(this));
        }
    }
}
</script>