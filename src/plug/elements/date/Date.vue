<template>
    <div>
        <el-time-select
            v-if="mixin_type(item) === 'date-time'"
            v-model="item.value"
            :picker-options="(item.config && item.config.pickerOptions) || {
                start: '06:00',
                step: '00:15',
                end: '22:00'
            }"
            @change="change"
            :style="mixin_style(item.style, item.value, item.data)"
            :placeholder="item.placeholder">
        </el-time-select>
        <el-date-picker
            v-else-if="mixin_type(item) === 'date-datetime'"
            v-model="item.value"
            type="datetime"
            @change="change"
            :style="mixin_style(item.style, item.value, item.data)"
            :placeholder="item.placeholder">
        </el-date-picker>
        <el-date-picker
            v-else
            v-model="item.value"
            type="date"
            @change="change" 
            :style="mixin_style(item.style, item.value, item.data)"
            :placeholder="item.placeholder">
        </el-date-picker>
    </div>
</template>
<script>
import base from '../../mixins/base.js';
export default {
    props: ['item'],
    mixins: [base],
    name: 'fddate',
    data() {
        return {}
    },
    methods: {
        change() {
            this.mixin_event({
                type: 'change',
                prop: this.item.prop,
                value: this.item.value
            })
        }
    },
    created() {
        if (this.item.value === void 0) {
            this.$set(this.item, 'value', '')
        }
        this.item.$data[this.item.prop] = this.item.value
        this.mixin_config('date') 
    }
}
</script>
