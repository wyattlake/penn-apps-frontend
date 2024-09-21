
<style>
  :global(body) {
    font-family: Arial, sans-serif;
    line-height: 1.6;
  }
</style>


<script>
    import Typewriter from 'svelte-typewriter';
  </script>
  
  <main class="container mx-auto px-4 py-8">
    <header class="flex justify-between items-center mb-2">
        <div class='logo'>
            <svg xmlns="http://www.w3.org/2000/svg" width="150" height="150" viewBox="0 0 400 100">
                <g id="Group_34" data-name="Group 34" transform="translate(-140 -300)">
                  <text id="mtrx" transform="translate(203 356)" font-size="80" font-family="Inter-SemiBold, Inter" font-weight="600"><tspan x="0" y="0">mtrx</tspan></text>
                  <text id="_" data-name="[" transform="translate(140 392)" fill="#95e398" font-size="200" font-family="Inter-Light, Inter" font-weight="300"><tspan x="0" y="0">[</tspan></text>
                  <text id="_2" data-name="]" transform="translate(383 392)" fill="#95e398" font-size="200" font-family="Inter-Light, Inter" font-weight="300"><tspan x="0" y="0">]</tspan></text>
                </g>
        </div>
      </header>    
    <Typewriter mode="loop" cursor={false}>
      <h2 class="text-2xl mb-4">Building data analytics solutions for 
        <span class="text-blue-500">small businesses</span>
      </h2>
      <h2 class="text-2xl mb-4">Building data analytics solutions for
        <span class="text-green-500">nonprofits</span>
      </h2>
      <h2 class="text-2xl mb-4">Building data analytics solutions for
        <span class="text-purple-500">innovators</span>
      </h2>
    </Typewriter>
    
    <p class="mt-8">
      This is a simple home page with a typing animation. The text above will 
      continuously loop through different phrases.
    </p>
</main>
