<script context="module">
  import { GraphQLClient } from 'graphql-request';
  export async function load(ctx) {
    const graphcms = new GraphQLClient(
      'https://api-eu-central-1.graphcms.com/v2/ck8sn5tnf01gc01z89dbc7s0o/master',
      {
        headers: {},
      }
    )
    const { product } = await graphcms.request(
      `query ProductPageQuery($slug: String!) { 
        product(where: { slug: $slug }) {
          name
          description
          price
        }
      }`,
      {
        slug: ctx.page.params.slug,
      }
    )
    return {
      props: {
        product,
      },
    }
  }
</script>

<script>
  export let product
</script>

<svelte:head>
  <title>{product.name}</title>
</svelte:head>

<h1>{product.name}</h1>
<p>{product.description}</p>
<p>${product.price / 100}</p>
