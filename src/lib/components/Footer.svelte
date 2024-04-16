<script>
  import { footerSections } from "$lib/data/footer-links";
</script>

<div
  class="bg-fw-darkblue text-white flex flex-col padding-x pt-12 pb-16 gap-8 lg:gap-16 xl:gap-28 sm:flex-row"
>
  <div class="flex flex-col justify-between">
    <h1 class="text-white">Ecommerce</h1> <!-- Reemplazar el logo con texto "Ecommerce" y cambiar el color a blanco -->

    <span class="text-fw-darkgrey hidden sm:block">
      desarrollado por Cristian Rojas.
    </span>
  </div>
  {#each footerSections as section}
    <div class="flex flex-col gap-5">
      <span class="font-semibold text-lg"> Products </span>
      <div class="flex flex-col gap-3">
        {#each section.links as link}
          <button class="cursor-pointer w-min whitespace-nowrap">
            {link.name}
          </button>
        {/each}
      </div>
    </div>
  {/each}
  <span class="text-fw-darkgrey block sm:hidden">
    desarrollado por Cristian Rojas.
  </span>
</div>
