<template>
    <div>
        <h2>{{botObj.bot}}</h2>
        <p>Attack:{{botObj.attack}}</p>
        <p>Health:{{botObj.health}}</p>
        <button @click='selectBot()'>Select</button>
        <button @click='retireBot(index)'>Retire</button>
        <hr>
    </div>
</template>

<script>
export default {
    props: ['botObj', 'index', 'retireBot', 'selectBot']
}
</script>
