<template>
    <div class="wrapp">
        <input type="text" id="inp" v-model="num"/>
        <div id="num1">{{ num }}</div>
        <div id="num2">{{ num }}</div>
        <div id="num3">{{ num }}</div>
        <div id="num4">{{ num }}</div>
        <div id="num5">{{ num }}</div>
        <div id="num6">{{ num }}</div>
        <div id="num7">{{ num }}</div>
        <div id="num8">{{ num }}</div>
        <div id="num9">{{ num }}</div>
        <div id="num10">{{ num }}</div> 
    </div>
</template>

<script>
export default {
    name: 'Increment',
    data: {
    },
    props: ['num']
}
</script>

<style scoped> 
#inp {
    z-index: 999 !important;
    position: fixed;
    top: 0;
    left: 45vw;
}
.wrapp > div {
    z-index: -1 !important;
}
#num1 {
    transform: translate(1000px, 120px)rotate(8deg)scale(1.8);
}
#num2 {
    transform: translate(1900px, -910px)rotate(-18deg)scale(3);
}
#num3 {
    transform: translate(100px, 120px)rotate(8deg)scale(.6123);
}
#num4 {
    transform: translate(2400px, 120px)rotate(8deg)scale(5);
}
#num5 {
    transform: translate(1300px, 280px)rotate(8deg)scale(1.7);
}
#num6 {
    transform: translate(1000px, 620px)rotate(10deg)scale(3);
}
#num7 {
    transform: translate(3000px, -620px)rotate(-20deg)scale(13);
}
#num8 {
    transform: translate(2020px, 20px)rotate(13deg)scale(17);
}
#num9 {
    transform: translate(1100px, 120px)rotate(44deg)scale(22);
}
#num10 {
    transform: translate(100px, 0px)rotate(0deg)scale(60);
}
</style>
