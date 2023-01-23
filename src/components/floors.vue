<template>
    <div class="elevator__floors">
        <elevator-floor
            v-for="floor in floors" :key="floor.id"
            :shafts="shafts"
            :floor="floor"
            :floors="floors"
        />
    </div>
</template>

<script>
    import elevatorFloor from '@/components/floor.vue'
    export default {
        components: {
            elevatorFloor,
        },
        props: {
            shafts: {
                type: Array,
                required: true,
            },
            floors: {
                type: Array,
                required: true,
            },
        },
    }
</script>

<style lang="sass">
.elevator__floors
    position: relative
    z-index: 0
    bottom: 10px
    width: 100%
    height: 100%
    display: flex
    align-items: center
    flex-direction: column-reverse
</style>