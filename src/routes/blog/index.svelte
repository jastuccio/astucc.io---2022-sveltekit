<!-- lang="ts" -->
<script context="module">
	/* * glob imports come from vite
	 * https://vitejs.dev/guide/features.html#glob-import
	 */
	const localPosts = import.meta.glob('./*.{md,svx}');

	let body = [];
	for (let path in localPosts) {
		body.push(
			localPosts[path]().then(({ metadata }) => {
				return { path, metadata };
			})
		);
	}

	export const load = async () => {
		const posts = await Promise.all(body);
		return {
			props: {
				posts
			}
		};
	};
</script>

<script>
	export let posts; // receive posts
</script>

<ul>
	{#each posts as { path, metadata: { title, date } }}
		<li>
			<a href={`/blog${path.replace(/\.\.*\w*/gi, '')}`}>{title}</a>
		</li>
	{/each}
</ul>

<!-- 
<script>
	export let posts = [];
	// console.log('unsorted: ', localPosts);

	const postsSortedByDate = posts.slice().sort((post1, post2) => {
		return new Date(post2.metadata.date) - new Date(post1.metadata.date);
	});
	JSON.stringify(postsSortedByDate);
	// console.log('sorted: ', postsSortedByDate);
</script>

<h1>Blog</h1>

{#each postsSortedByDate as { path, metadata: { title, tags, date } }}
	<li>
		<a href={`/blog${path.replace(/\.\.*\w*/gi, '')}`}>{title}</a>

		<p>
			{#each tags as tag}
				<a class="tag" href={`/tags/${tag}`}>#{tag}</a>
			{/each}
		</p>
		<p>{new Date(date).toDateString()}</p>
	</li>
{/each}

<script context="module">
	/* * glob imports come from vite
	 * https://vitejs.dev/guide/features.html#glob-import
	 */
	const localPosts = import.meta.glob('./*.{md,svx}');

	let body = [];
	for (let path in localPosts) {
		body.push(
			localPosts[path]().then(({ metadata }) => {
				return { path, metadata };
			})
		);
	}

	export const load = async () => {
		const posts = await Promise.all(body);

		return {
			props: {
				posts
			}
		};
	};
</script>


 -->
<style>
	p {
		margin: 0;
	}
	li {
		margin-bottom: 20px;
	}
	.tag {
		text-decoration: none;
		margin-right: 10px;
		color: #555;
	}
	.tag:hover {
		color: blue;
	}
</style>
