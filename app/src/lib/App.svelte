<script>
    import MathFieldv1 from "$lib/MathFieldv1.svelte";
    import MathFieldv2 from "$lib/MathFieldv2.svelte";

    let value1 = $state('\\begin{pmatrix}\\placeholder[answer]{} & 2\\\\ 3 & 4\\end{pmatrix}');
    let value2 = $state('\\begin{pmatrix}\\placeholder[answer]{} & 2\\\\ 3 & 4\\end{pmatrix}');
    let answer1 = $state();
	let mathEle1 = $state();

    let prompts2 = $state();
    let getPromptValue2 = $state();
    let answer2 = $derived(getPromptValue2('answer'));
	$inspect(answer2);
    $effect(()=>{
        value1 = value1;
        answer1 = mathEle1.getPromptValue('answer');
  })
</script>

<div>
Version 1:
<MathFieldv1 bind:value={value1} bind:node={mathEle1} read-only></MathFieldv1>
<p>Current LaTeX: {value1}</p>

<p>Prompt (answer):  {answer1}</p>
</div>


<!-- <div>
Version 2:
<MathFieldv2 bind:value={value2} bind:prompts={prompts2} bind:getPromptValue={getPromptValue2} read-only></MathFieldv2>
<p>Current LaTeX: {value2}</p>

<p>Prompt (answer):  {answer2}</p>
<p>Prompts2:  {prompts2}</p>
<p>Answer:  {answer2}</p>
</div>
 -->

