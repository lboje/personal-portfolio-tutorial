<script context="module">
    console.log('does it work here?');
    export const prerender = true;

    export async function load({ page, fetch, session, context }) {
        console.log('does it work?');
        // Retrieve data about the post
        const pageNum = +page.params?.page || 1;
        const url = `/posts.json?page=${pageNum}`;
        console.log(url);
        const res = await fetch(url);

        // If the response is successful, render the post
        if (res.ok) {
            const { pages, posts } = await res.json();
            return {
                props: {
                    pages: new Array(pages).fill(0).map((x, idx) => idx + 1),
                    posts,
                    pageNum
                }
            };
        }

        // Otherwise, return an error
        return {
            status: res.status,
            error: new Error(`Could not load ${url}`)
        };
    }
</script>

<script>
    import BlogSnippets from '../../components/BlogSnippets.svelte';

    export let posts;
    export let pages;
    export let pageNum;

</script>

<div class="flex-grow bg-gray-50">
    <BlogSnippets title="The Blog" {posts} {pages} {pageNum} />
</div>
