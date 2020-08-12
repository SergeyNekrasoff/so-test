<template>
    <div>
        <div class="tree">
            <ul class="tree-list">
                <node-tree :node="treeArr"></node-tree>
            </ul>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import NodeTree from './NodeTree.vue';

@Component({
    components: { 
        NodeTree 
    }
})

export default class Tree extends Vue {
    @Prop({ type: Array, required: true }) list!: Array<object>;

    get treeArr(): Array<object> {
        let root: any = [];
        const idMapping = this.list.reduce((acc: any, el: any, i: number) => {
            acc[el.id] = i;
            return acc
        }, {})

        this.list.forEach((el: any) => {
            if (el.parentId === 0) {
                root = el;
                return;
            }
            const parentEl: any = {} = this.list[idMapping[el.parentId]];
            parentEl.children = [...(parentEl.children || []), el];
        });
        
        return root;
    }
}
</script>

<style lang="scss">
.tree-list {
    width: 600px;
    min-height: calc(100vh - 200px);
    padding: 16px;
    border: 1px solid #ccc;

    &__sub {
        margin-left: 20px;
    }
}

.node-tree {
    padding: 8px;
    margin: 16px 0 0 8px;
    height: 150px;
    text-align: left;

    &__text {
        height: 50px;
    }

    .label {
        display: inline-block;
    }
}
</style>