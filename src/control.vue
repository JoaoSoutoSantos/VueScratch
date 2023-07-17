<script setup>
import { Panel, useVueFlow } from '@vue-flow/core'

const flowKey = 'example-flow'

const { nodes, addNodes, setNodes, setEdges, dimensions, setTransform, toObject } = useVueFlow()

function onSave() {
  localStorage.setItem(flowKey, JSON.stringify(toObject()))
}

function onRestore() {
  const flow = JSON.parse(localStorage.getItem(flowKey))

  if (flow) {
    const [x = 0, y = 0] = flow.position
    setNodes(flow.nodes)
    setEdges(flow.edges)
    setTransform({ x, y, zoom: flow.zoom || 0 })
  }
}

function onAdd() {
  const id = nodes.value.length + 1

  const newNode = {
    id: `random_node-${id}`,
    label: `Node ${id}`,
    position: { x: Math.random() * dimensions.value.width, y: Math.random() * dimensions.value.height },
  }

  addNodes([newNode])
}
</script>

<template>
  <Panel position="top-right" class="save-restore-controls">
    <button style="background-color: #33a6b8" @click="onSave" class="px-3 py-1 mx-1 text-white rounded">Salvar</button>
    <button style="background-color: #113285" @click="onRestore"
      class="px-3 py-1 text-white rounded mx-1">Restaurar</button>
    <!-- <button style="background-color: #6f3381" @click="onAdd" class="px-3 py-1 text-white rounded">Adicionar Nó</button> -->
  </Panel>
</template>
