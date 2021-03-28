<template>
    <h1>Lifecycle hooks</h1>
</template>

<script>
    import { onMounted } from 'vue'

    // export default {
    //     mounted () {
    //         console.log('Mounted!')
    //     }
    // }

    export default {
        setup () {
            onMounted(() => {
                console.log('Mounted composition API')
            })
        }
    }
</script>