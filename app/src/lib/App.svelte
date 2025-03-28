<script lang="ts">
    import MathFieldv2 from "$lib/MathFieldv2.svelte";

    // let value = $state('\\displaystyle\\begin{bmatrix}\\placeholder[answer00]{1} & \\placeholder[answer01]{}\\\\ 3 & 4\\end{bmatrix}');
    let value = $state('\\begin{bmatrix}\\placeholder[answer00]{1} & \\placeholder[answer01]{\\phantom{1}}\\\\ 3 & 4\\end{bmatrix}');

    let prompts = $state();
    // let getPromptValue2 = $state();
    let answer2 = $state();
	$inspect(prompts);
</script>



<div>
Version 2:
<MathFieldv2 bind:value={value} bind:prompts={prompts} smart-mode="true" default-mode="inline-math"></MathFieldv2>
<p>Current LaTeX: {value}</p>

<p>Prompt (answer):  {answer2}</p>
<p>Prompts2:  {prompts}</p>
<p>Answer:  {answer2}</p>
<button onclick={()=>{
    prompts["answer00"] = "x+1";
    }}>Set value [0,0] to "x+1"</button>
</div>


