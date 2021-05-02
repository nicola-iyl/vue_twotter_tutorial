<template>
    <div class="user-profile">
        <div class="user-panel">
            <h4>@{{ user.username }}</h4>

            <div><strong>Followers:</strong> {{ followers }}</div>
            <div v-if="user.isAdmin" class="user-profile">
                Admin
            </div>
            <div v-else class="user-profile">
                Not Admin
            </div>
            <div class="user-twotters">
                <div v-for="twott in user.twotters" :key="twott.id" class="twotter-item">
                    {{ twott.content }}
                </div>
            </div>
            <button @click="followUser">Follow</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "UserProfile",
        data(){
            return{
                followers: 0,
                user: {
                    id: 1,
                    username: 'Nicola Tamburini',
                    firstName: 'Nicola',
                    lastName: 'Tamburini',
                    email: 'nicola.tamburini@fjstudio.com',
                    isAdmin: false,
                    twotters: [
                        { id: 1, content: 'contenuto tweet uno'},
                        { id: 2, content: 'contenuto tweet due'}
                    ],
                }
            }
        },
        computed: {
            fullName()
            {
                return this.user.firstName + '' + this.user.lastName;
            }
        },
        //guarda il cambiamento di alcune variabile ed esegue qualcosa
        watch:{
            followers(newFollowerCount,oldFollowerCount)
            {
                if(oldFollowerCount < newFollowerCount)
                {
                    console.log(this.user.username + ' ha guadagnato un follower')
                }
            }
        },
        methods:{
            followUser()
            {
                this.followers++;
            }
        },
        //viene eseguito la prima volta che il componente viene istanziato
        //posto dove chiamare le api
        mounted()
        {
            this.followUser();
        }
    }
</script>

<style scoped>

</style>
