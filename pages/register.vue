<template>
    <div id="register">
        <div class="w-1/2 mx-auto">
            <div class="w-full flex flex-col mt-2">
                <label>Name</label>
                <input type="text" class="rounded border-gray-300 border p-2" v-model="name"/>
            </div>
            <div class="w-full flex flex-col mt-2">
                <label>Email</label>
                <input type="text" class="rounded border-gray-300 border p-2" v-model="email"/>
            </div>
            <div class="w-full flex flex-col mt-2">
                <label>Password</label>
                <input type="password" class="rounded border-gray-300 border p-2" v-model="password"/>
            </div>
            <div class="w-full flex flex-col mt-2">
                <label>Confirm Password</label>
                <input type="password" class="rounded border-gray-300 border p-2" v-model="confirm_password"/>
            </div>
            <div class="w-full flex flex-col mt-2">
                <button class="rounded text-white bg-blue-500 cursor-pointer px-5 py-2" v-on:click="register()">Register</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            name: '',
            email: '',
            password: '',
            confirm_password: ''
        }
    },

    methods: {
        register(){
            this.$axios.$get('https://laravel-api.521.test/sanctum/csrf-cookie')
                .then( function(){
                    this.$axios.$post('https://laravel-api.521.test/register', {
                        name: this.name,
                        email: this.email,
                        password: this.password,
                        confirm_password: this.confirm_password
                    })
                    .then( function( response ){
                        this.$auth.loginWith( 'laravelSanctum', {
                            data: {
                                email: this.email,
                                password: this.password,
                                confirm_password: this.confirm_password
                            }
                        })
                    }.bind(this));
                }.bind(this))

        }
    }
}
</script>