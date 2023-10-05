<!---- BAR ---------->


<!------------------->
<!---- CODE JS ------>
<!------------------->
<script>
    export let top = "0";
    export let left = "0";
	export let height = "20";
	export let width = "100";
    export let pLoad = 0.7;
    let pLoadOld = pLoad;
    export let pFore = 0.3;
    export let zMin = 1;
    export let cBack = "#34302D";
    export let cLoad = "#8CBFF3";
    export let cFore = "#246ABA";
    let cCursor = cLoad;
    let onBar = false;
    let onBarClick = false;

    function I(name) { return document.getElementById(name); }
	
	function mouseClick(event) {
        if (!onBar) { pLoadOld = pLoad; }
        pFore = (event.x - left)/width;
        pLoadOld = pFore;
        onBar = true;
        cCursor = cFore;
    }
    function mouseMove(event) {
        if (!onBar) { pLoadOld = pLoad; }
        if (!onBarClick) {
            pLoad = (event.x - left)/width;
            onBar = true;
            cCursor = cLoad;
        }
        else {
            pFore = (event.x - left)/width;
            pLoad = pFore;
            pLoadOld = pFore;
            onBar = true;
            cCursor = cFore;
        }
    }
    function mouseOut(event) {
        onBar = false;
        pLoad = pLoadOld;
    }
    function mouseDown(event) {
        onBarClick = true;
    }
    function mouseUp(event) {
        onBarClick = false;
    }
</script>


<!------------------->
<!---- CODE HTML ---->
<!------------------->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-mouse-events-have-key-events -->
<div on:click={mouseClick} on:mouseover={mouseMove} on:mousemove={mouseMove} on:mouseout={mouseOut} on:mousedown={mouseDown} on:mouseup={mouseUp} class="bar" style="top:{top}px;left:{left}px;z-index:{zMin};background:{cBack};height:{height}px;width:{width}px;">
    <div class="bar" style="z-index:{zMin+1};background:{cLoad};height:{height}px;width:{pLoad*width}px;"></div>
    <div class="bar" style="z-index:{zMin+2};background:{cFore};height:{height}px;width:{pFore*width}px;"></div>
    <div class="barCursor" style="top:-{0.5*height}px;left:{pLoad*width -height}px;z-index:{zMin+3};background:{cCursor};height:{2*height}px;width:{2*height}px;display:{onBar ? 'block':'none'}"></div>
</div>


<!------------------->
<!---- CODE CSS ----->
<!------------------->
<style>
	.bar
	{
		margin: 0;
		padding: 0;
        position: absolute;
        cursor: pointer;
	}
    .barCursor
    {
        margin: 0;
        padding: 0;
        position: absolute;
        cursor: pointer;
        border-radius: 100%;
    }
</style>