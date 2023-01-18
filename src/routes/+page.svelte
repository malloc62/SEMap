<script>

var docDimensions = [0,0];
var mapDimensions = [0,0]; 
var viewPos       = [0,0];
var pos           = [0,0];
var posMouse      = [0,0];
var posMouseHook  = [0,0];

var isMouse = false;

function mouseDown(e) {
    isMouse = true;
};

function mouseUp(e) {
    isMouse = false;
};

function mouseMove(e) {
    posMouse = [e.clientX,e.clientY];    

    if (isMouse) {
        for (var i = 0; i < 2; i++) {     
            var deltaPos = posMouse[i] - posMouseHook[i];
            pos[i] += deltaPos;

            var viewOffset = mapDimensions[i] - docDimensions[i];
            viewPos[i] = (pos[i] - viewOffset / 2) + 'px';
        }
    }

    posMouseHook = posMouse;

};
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

</style>

<svelte:window on:mousedown={mouseDown} on:mouseup={mouseUp} on:mousemove={mouseMove}/>
 
<div id='ui-wrap'>
    <div>
        Mouse to pan or move map <br/>
    </div> 
</div>

<div class='document'  bind:clientWidth={docDimensions[0]} bind:clientHeight={docDimensions[1]} >
    <div class='area' bind:clientWidth={mapDimensions[0]} bind:clientHeight={mapDimensions[1]} style='top: {viewPos[1]}; left: {viewPos[0]}'>
        <img src='/map.svg'  >
    </div>
</div>
