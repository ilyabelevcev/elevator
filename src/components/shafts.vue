<template>
    <div class="elevator__shafts">
        <elevator-shaft
            v-for="shaft in shafts" :key="shaft.id"
            :shaft="shaft"
        />
    </div>
</template>

<script>
    import elevatorShaft from '@/components/shaft.vue'
    export default {
        components: {
            elevatorShaft,
        },
        props: {
            shafts: {
                type: Array,
                required: true,
            },
        }
    }
</script>

<style lang="sass">
.elevator__shafts
    position: absolute
    z-index: 1
    height: 100%
    width: 90%
    left: 5%
    display: flex
    align-items: center
    flex-direction: row
</style>