<template>
    <div>
        <b-nav tabs>
            <b-nav-item disbaled>Counter : {{numCorrect}}/{{numTotal}}</b-nav-item>
            <b-nav-item disbaled >Total : 10</b-nav-item>
        </b-nav>
    </div>
</template>

<script>
   
    export default {
        props:["numCorrect",
        "numTotal"
        ]
    }
</script>

<style scoped>

div {
  background-color: yellow;
  margin-bottom: 25px;
}

</style>