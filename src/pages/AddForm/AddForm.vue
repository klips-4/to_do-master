<template src="./template.html"/>

<script>


    import SourceService from "@/services/SourceService";

    export default {
        name: "AddForm",
        data() {
            return {
                name,
                source: new SourceService({endpoint: 'Task'})
            }

        },
        beforeMount() {
            this.source.create().then((result) => {
                if(result.success) {
                    this.taskData = {...result.data};
                }
            });
        },

        methods: {
            submit() {
                const rec ={...this.taskData, description: this.name};
                    this.source.update(rec).then((result) => {
                        if (result.success) {
                            this.name = '';
                            this.$emit('submit');
                            this.$emit('close');
                        }
                    });
            },
        }


    }
</script>

<style scoped src="./style.less" lang="less"></style>