<template>
    <ul>
        <li>
            <button :class="className" @click="$emit('complete')"><i class="far fa-circle"></i> {{ task.title }}</button>
            <button @click="$emit('remove')"><i class="far fa-trash-alt"></i></button>
            <!-- Emit allows you to work script on Parent component  -->
        </li>
    </ul>
</template>

<script>
    export default {
        props: ['task'],
        computed: {
            className() {
                let classes = ['toggle'];
                if (this.task.completed) {
                    classes.push('toggle-completed')
                }
                return classes;
            }
        }
    }
</script>