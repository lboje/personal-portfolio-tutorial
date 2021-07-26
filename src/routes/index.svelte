<script context="module">
    export const prerender = true;

    export async function load({ page, fetch, session, context }) {
        console.log("hello");
        let res = await fetch('/posts/recent-posts.json');

        return {
            props: {
                posts: await res.json()
            }
        };
    }
</script>

<script>
    import Hero from '../components/Hero.svelte';
    import BlogSnippets from '../components/BlogSnippets.svelte';

    export let posts;
</script>

<Hero
    title="Lucas Boje"
    subTitle="🐟🐠🐡 Bit of a wreck right now, don't mind the construction. 🐟🐠🐡"
/>

<BlogSnippets {posts} title="Recent Posts" />
