<template src="./template.html"/>

<script>


    export default {
        name: "TaskRender",
        props: ['data'],
        data() {
            return {

            }

        },

        methods: {
            deleteTask(id) {
                this.$emit('deleted', id)
            },

            completeTask(data) {
                this.$emit('completeTask', data)
            },

            dateFormatter(date) {
                date = new Date(date);
                return date.toLocaleString('ru', {
                    year: 'numeric',
                    month: 'long',
                    day: 'numeric'
                });
            }
        }


    }
</script>

<style scoped src="./style.less" lang="less"></style>