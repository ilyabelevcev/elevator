<template>
    <div class="app__container">
        <elevator-shafts 
            :shafts="shafts"
        />
        <elevator-floors 
            :shafts="shafts"
            :floors="floors"
        />
    </div>
</template>

<script>
    import elevatorShafts from '@/components/shafts.vue'
    import elevatorFloors from '@/components/floors.vue'
    export default {
        components: {
            elevatorShafts,
            elevatorFloors,
        },
        data() {
            return {
                shafts: [
                    {
                        id: 0,
                        distanceElevator: 0,
                        transitionElevator: 0, 
                        currentFloor: 0,
                        desiredFloor: 0,
                        isActiveElevator: false,
                        isActiveSleep: false,
                        upElevator: false,
                        downElevator: false,
                    },
                ],
                floors: [
                    {id: 0, num: 1, isFreeFloor: true, isActiveMove: false, isActiveSleep: false},
                    {id: 1, num: 2, isFreeFloor: true, isActiveMove: false, isActiveSleep: false},
                    {id: 2, num: 3, isFreeFloor: true, isActiveMove: false, isActiveSleep: false},
                    {id: 3, num: 4, isFreeFloor: true, isActiveMove: false, isActiveSleep: false},
                    {id: 4, num: 5, isFreeFloor: true, isActiveMove: false, isActiveSleep: false},
                ],
            }
        },
    }
</script>

<style lang="sass">
*,*::before,*::after 
    box-sizing: border-box
    padding: 0
    margin: 0
    border: 0
#app,
body
    width: 100%
    height: 100vh
    overflow: hidden
#app
    font-family: Avenir, Helvetica, Arial, sans-serif

.app__container
    position: relative
    width: 100%
    height: 100%
    bottom: 0

@keyframes indication 
    0%,100%
        opacity: 1
    50%
        opacity: 0.5

</style>
