<template>
    <div>
        <Number
            label="PointId"
            v-model="value.pointId"
            :editMode="editMode"
        />
        <String
            label="UserId"
            v-model="value.userId"
            :editMode="editMode"
        />
        <Number
            label="PointBalance"
            v-model="value.pointBalance"
            :editMode="editMode"
        />
        <Number
            label="StandardSignupPoint"
            v-model="value.standardSignupPoint"
            :editMode="editMode"
        />
        <Number
            label="KtSignupPoint"
            v-model="value.ktSignupPoint"
            :editMode="editMode"
        />
        <Number
            label="Amount"
            v-model="value.amount"
            :editMode="editMode"
        />
        <Date
            label="UsedAt"
            v-model="value.usedAt"
            :editMode="editMode"
        />
        <v-row class="ma-0 pa-0">
            <v-spacer></v-spacer>
            <v-btn width="64px" color="primary" @click="save">
                저장
            </v-btn>
        </v-row>
    </div>
</template>


<script>
import BaseEntity from './base-ui/BaseEntity.vue'

export default {
    name: 'Point',
    mixins:[BaseEntity],
    components:{
    },
    
    data: () => ({
        path: "points",
        value: {
        }
    }),
    created(){
    },
    computed:{
    },
    methods: {
    },
}
</script>
