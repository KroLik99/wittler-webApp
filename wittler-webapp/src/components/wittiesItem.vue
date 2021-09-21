<template>
    <div class="witties-item" @click="favouriteWittie(wittie.id)">
        <div class="user-profile__witties">
            <div class="witties-item__user">
                @{{username}}
            </div>
            <div class="witties-item__content">
                {{ witties.content }}
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: "WittiesItem",
    props: {
        username: {
            type: String,
            required: true
        },
        witties: {
            type: Object,
            required: true
        }
    },
    methods: {
        favouriteWittie(id){
            this.$emit("favourite", id)
        }
    }
};
</script>

<style>
.witties-item {
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    box-sizing:border-box;
    cursor:pointer;
    transition:all 0.25s ease;
}

.witties-item:hover {transform: scale(1.1, 1.1);}

.witties-item__user {
    font-weight: bold;
}

</style>