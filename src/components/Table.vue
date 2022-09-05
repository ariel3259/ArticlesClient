<script>
    /**
     * fields {Array<object>}
     * fields {Array<object>}
     */
    export default {
        props: {
            fields: Array,
            data: Array,
            deleteItem: Function,
            togleModifyItem: Function
        }
    }
</script>

<template>
    <table class="table table-stripped table-bordered">
        <thead>
            <tr>
                <th v-for="(field, index) in fields" :key="index">{{field}}</th>
                <th>Acciones</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="element in data" :key="element.id">
                <td v-for="(value, index) in Object.values(element)" :key="index">{{value}}</td>
                <td>
                    <div class="btn-group">
                        <button class="btn btn-danger" @click="deleteItem(element.id)">Delete</button>
                        <button class="btn btn-primary" @click="togleModifyItem(element.id)">Modificar</button>
                    </div>
                </td>
            </tr>
            <tr v-if="data.length === 0">
                <td colspan="100%" :style="{textAlign: 'center'}">No hay datos</td>
            </tr>
        </tbody>
    </table>
</template>

