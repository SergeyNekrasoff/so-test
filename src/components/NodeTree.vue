<template>
    <li class="node-tree">
        <div class="node-tree__text">
            <label :for="node.id">
                <input 
                    type="checkbox" 
                    v-model="node.checked" 
                    :disabled="node.parentId === 0 && !allChildren"
                    :id="node.id"
                    @change="onChange(node)" />
                {{ node.name }}
                {{ node.parentId === 0 && !allChildren }}
            </label>
        </div>    

        <ul class="tree-list__sub" v-if="node.children && node.children.length">
            <node 
                v-for="child in node.children" 
                :node="child" 
                :key="child.id">
                <div class="node-tree__text">
                    <label :for="node.id">
                        <input 
                            type="checkbox" 
                            v-model="node.checked"
                            :disabled="node.parentId === 0 && !allChildren"
                            :id="node.id"
                            @change="onChange(node)" />
                        {{ node.name }}
                    </label>
                </div>
            </node>
        </ul>
    </li>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component({
    name: 'node'
})

export default class Tree extends Vue {
    @Prop({ type: Object, required: true }) node!: Object;

    public allChildren: boolean = true

    public onChange(node: any): void {
        if (node.parentId > 0 && !node.checked) {
            this.allChildren = false
        }
    }
}
</script>