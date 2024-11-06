<script setup>

    //import ref and onMounted
    import { ref, onMounted } from 'vue';

    //import api
    import api from '../../api';

    //define state
    const members = ref([]);

    //method fetchDataPosts
    const fetchDataPosts = async () => {

        //fetch data 
        await api.get('/api/members')

        .then(response => {

            //set response data to state "posts"
            members.value = response.data.data

        });
    }

    //run hook "onMounted"
    onMounted(() => {

        //call method "fetchDataPosts"
        fetchDataPosts();
    });

</script>

<template>
    <div class="container mx-auto mt-5 mb-5">
        <div class="flex justify-end mb-3">
            <router-link :to="{ name: 'members.create' }" class="btn btn-success btn-sm">ADD NEW POST</router-link>
        </div>
        <div class="card shadow-lg">
            <div class="card-body">
                <table class="table w-full">
                    <thead>
                        <tr class="bg-primary text-white">
                            <th scope="col">Id</th>
                            <th scope="col">Class</th>
                            <th scope="col">First Name</th>
                            <th scope="col">Last Name</th>
                            <th scope="col">Email</th>
                            <th scope="col">Gender</th>
                            <th scope="col">Address</th>
                            <th scope="col" style="width:15%">Actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-if="members.length == 0">
                            <td colspan="8" class="text-center">
                                <div class="alert alert-error">
                                    Data Belum Tersedia!
                                </div>
                            </td>
                        </tr>
                        <tr v-else v-for="(member, index) in members" :key="index">
                            <td>{{ member.id }}</td>
                            <td>{{ member.class.id }}</td>
                            <td>{{ member.first_name }}</td>
                            <td>{{ member.last_name }}</td>
                            <td>{{ member.email }}</td>
                            <td>{{ member.gender }}</td>
                            <td>{{ member.address }}</td>
                            <td class="text-center">
                                <router-link :to="{ name: 'members.edit', params:{id: member.id} }" class="btn btn-primary btn-xs mr-2">EDIT</router-link>
                                <button class="btn btn-error btn-xs">DELETE</button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>