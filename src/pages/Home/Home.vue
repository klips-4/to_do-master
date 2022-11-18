<template src="./template.html"/>

<script>
    import {AuthHelpers} from "@/helpers/AuthHelpers";
    import AddForm from "@/pages/AddForm/AddForm";
    import SourceService from "@/services/SourceService";
    import TaskRender from "@/components/Task/TaskRender";

    export default {
        name: "HomePage",
        components: {AddForm, TaskRender},

        data() {
            return {
                addFormVisible: false,
                items: [],
                onlyActive: '1',
                source: new SourceService({endpoint: 'Task'})

            }
        },
        beforeMount() {
            this.getItems()
        },

        methods: {
            logout() {
                AuthHelpers.logout();
            },
            changeAddFormVisible() {
                this.addFormVisible = !this.addFormVisible;
            },
            getItems() {
                this.source.list({onlyActive: Number(this.onlyActive)}).then((result) => {
                    if (result.success) {
                        this.items = result.data;
                    }
                });
            },
            deleteTask(id) {
                this.source.delete(id).then((res) => {
                    if (res.success) {
                        this.getItems()
                    }
                });
            },
            completeTask(data) {
                console.log('hello')
                data.date_completed = new Date();
                this.source.update(data)
            },
            applyFilter() {
                this.getItems();
            },
            computed: {
                userName() {
                    const userData = AuthHelpers.getUserInfo();
                    return userData.surname + ' ' + userData.name[0] + '.';
                }
            },

        }
    }
</script>

<style scoped src="./style.less" lang="less"></style>