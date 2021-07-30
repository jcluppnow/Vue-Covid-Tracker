<!-- This will track title, data and time for the data. -->
<template>
    <div class="text-center">
        <h2 class="text-3xl font-bold">{{text}}</h2>
        <div class="text-2xl mt-4 mb-10">
            <!-- Call computed timestamp to process data date. -->
            {{ timeStamp }}
        </div>
    </div>
</template>

<script>
    import moment from 'moment'

    export default {
        name: 'DataTitle',
        props: ['text', 'dataDate'],
        computed: {
            timeStamp: function()
            {
                return moment(this.dataDate).format('MMMM Do YYYY, h:mm:ss a');
            }
        }
    }
</script>
