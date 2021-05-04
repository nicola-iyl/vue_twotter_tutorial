<template>
    <div class="row user-profile">
        <div class="col-md-6">
            <form @submit.prevent="createNewTwoot" :class="{'text-danger':newTwootCaractherCount > 100}">
                <h3>New Twooter ({{ newTwootCaractherCount }} / 100)</h3>
                <textarea id="newTwoot" class="form-control" v-model="newTwootContent"></textarea>
                <div class="mt-2">
                    <label for="twoot_type">Type</label>
                    <select id="twoot_type" class="form-control mt-2" v-model="selectedTwootType">
                        <option v-for="option in TwootTypes" :key="option.value" :value="option.value">{{ option.name }}</option>
                    </select>
                    <button class="btn btn-success mt-2">Twoot!</button>
                </div>
            </form>
        </div>
        <div class="col-md-6">
            <div class="card">
                <h4>@{{ user.username }}</h4>

                <div class="card-title">
                    <strong>Followers:</strong> {{ followers }}
                </div>
                <div class="card-body">
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
                    <TwootItem
                            v-for="twoot in user.twotters"
                            :key="twoot.id"
                            :username="user.username"
                            :twoot="twoot"
                            @favourite="toggleFavourite"
                    />
                    <button class="btn btn-primary" @click="followUser">Follow</button>
                </div>

            </div>
        </div>

    </div>
</template>

<script>
    import TwootItem from "./TwootItem"
    export default {
        name: "UserProfile",
        components: {TwootItem},
        componets: {TwootItem},
        data(){
            return{
                newTwootContent: '',
                selectedTwootType: 'instant',
                TwootTypes:[
                    { value: 'draft', name: 'Draft' },
                    { value: 'instant', name: 'InstantTwoot' },
                ],
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
            },

            newTwootCaractherCount()
            {
                return this.newTwootContent.length;
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
            },
            toggleFavourite( id ){
                console.log(id);
            },
            createNewTwoot()
            {
                if(this.newTwootContent && this.selectedTwootType !== 'draft')
                {
                    this.user.twotters.unshift({ id: this.user.twotters.length +1 ,content: this.newTwootContent});
                    this.newTwootContent = '';
                }
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
