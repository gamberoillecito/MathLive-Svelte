<script lang="ts">
    import MathFieldv2 from "$lib/MathFieldv2.svelte"
    import type {promptsDict} from "$lib/MathFieldv2.svelte"
    import {ComputeEngine} from  "@cortex-js/compute-engine"
    let value = $state('\\begin{bmatrix}\\placeholder[answer00]{1} & \\placeholder[answer01]{}\\\\ 3 & 4\\end{bmatrix}');

    let ce = new ComputeEngine();
    let prompts: promptsDict = $state({});
    // let getPromptValue2 = $state();
    let answer2 = $state();
	$inspect(prompts);
</script>



<div>
Matrix:
<MathFieldv2 bind:value={value}  bind:prompts={prompts} math-virtual-keyboard-policy="manual" menuItems={[]} smart-mode="false"></MathFieldv2>
<p>Current LaTeX: {value}</p>

<p>Prompts:  {prompts}</p>
<p>matrix[0][0]:  {prompts["answer00"]}</p>
<p>matrix[0][1]:  {prompts["answer01"]}</p>
<button onclick={()=>{
    prompts["answer00"] = "x+1";
    }}>Set value [0][0] to "x+1"</button>
</div>

<button
    onclick={()=>{
    console.log(ce.parse(prompts["answer00"]).N().print());
    }
    }> eval [0][0] </button>



<input type="text" bind:value={prompts["answer01"]}>