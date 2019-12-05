<script>
  import Product from "./Product.svelte";
  import CartItem from "./CartItem.svelte";
	import FamilyNode from "./FamilyNode.svelte";
	
	let y;

	$: console.log(y);

	let currentTitle = 'My App';

  let familyStructure = [
    {
      isParent: true,
      name: "Chris",
      children: [
        {
          isParent: true,
          name: "Moe",
          children: [
            {
              isParent: false,
              name: "Julie"
            }
          ]
        }
      ]
    },
    {
      isParent: true,
      name: "Ana",
      children: [
        {
          isParent: true,
          name: "Aimi",
          children: [
            {
              isParent: false,
              name: "Boruto"
            }
          ]
        }
      ]
    }
  ];

  let renderedComponent = {
    comp: Product,
    title: "Test Product",
    id: "p1"
  };

  function toggle() {
    if (renderedComponent.comp === Product) {
      renderedComponent = {
        comp: CartItem,
        title: "Another Product",
        id: "p2"
      };
    } else {
      renderedComponent = {
        comp: Product,
        title: "Test Product",
        id: "p1"
      };
    }
	}

	function switchTitle() {
		currentTitle = 'New Title';
	}
</script>

<style>
	div {
		height: 3000px;
	}
</style>

<svelte:window bind:scrollY={y} />
<svelte:body on:mouseenter />

<svelte:head>
	<title>{currentTitle}</title>
</svelte:head>

<button on:click={switchTitle}>Switch Title</button>

<div>
	<button on:click={toggle}>Toggle Display</button>

	<svelte:component
		this={renderedComponent.comp}
		title={renderedComponent.title}
		id={renderedComponent.id} />

	{#each familyStructure as familyMember}
		<FamilyNode member={familyMember} />
	{/each}
</div>