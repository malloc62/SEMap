<script>

let docW, mapW, docH, mapH;

var top = 0;
var left = 0;

var keys = {};

var vel = [0,0];
var pos = [0,0];

function keydown(e) {
    keys[e.key.toLowerCase()] = true;
};

function keyup(e) {
    keys[e.key.toLowerCase()] = false;
};

setInterval(function() {
    var isShift = keys['q'];
    vel[0] += ((keys['a'] ? 1 : 0) - (keys['d'] ? 1 : 0)) * (isShift ? 5 : 1);
    vel[1] += ((keys['w'] ? 1 : 0) - (keys['s'] ? 1 : 0)) * (isShift ? 5 : 1);

    vel[0] *= 0.9;
    vel[1] *= 0.9;

    pos[0] += vel[0];
    pos[1] += vel[1];

    left = (pos[0] - mapW/2 + docW/2) + 'px';
    top = (pos[1] - mapH/2 + docH/2) + 'px';
},10);
</script>

<style>
    .document {
        width: 100vw;
        height: 100vh;
        background: var(--dark-1);
    
        position: fixed;
    }

    .area {
        position: absolute;
    }

    #ui-wrap {
        display: flex;
        flex-direction: row;
        justify-content: space-between;

        width: calc(100vw - 20px);
        padding: 10px;

        z-index: 1;
    
        color: var(--light-1);
    }
    
    #ui-right {
        text-align: right;
    }

</style>

<svelte:window on:keydown={keydown} on:keyup={keyup}/>
 
<div id='ui-wrap'>
    <div>
        WASD to pan or move map (+ Q to speed up) <br/>
    </div> 
</div>

<div class='document'  bind:clientWidth={docW} bind:clientHeight={docH} >
    <div class='area' bind:clientWidth={mapW} bind:clientHeight={mapH} style='top: {top}; left: {left}'>
        <img src='/map.png'  >
    </div>
</div>
