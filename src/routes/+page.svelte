<script>
    import { onMount } from "svelte";
    import resume from "$lib/documents/Resume-Web.pdf";
    import Stats from "./components/stats.svelte";
    import Posts from "$lib/posts/posts.json";

    let latestPost = null;
    let postId = null;
    let allPosts = [];
    let title = "";
    let postDate = "";
    let postContent = "";

    onMount(() => {
        allPosts = Posts.posts;
        if (allPosts.length > 0) {
            latestPost = allPosts.reduce((max, item) => (item.postid > max.postid ? item : max));
            postId = latestPost.postid;
            title = latestPost.cardTitle;
            postDate = latestPost.cardDate;
            postContent = latestPost.cardContent;
        }
    });

    function changePost(postId) {
       
        let post = allPosts.find(post => post.postid === postId);

         
         postId = post.postid;
        title = post.cardTitle;
        postDate = post.cardDate;
        postContent = post.cardContent;
    }
</script>

<main class="container py-5">
    <section class="text-center mb-5">
        <h1 class="display-4 fw-bold">🧭 Market Ready: Mark Hansen</h1>
        <p class="lead">EXPERIENCED PRODUCT MANAGER & TECHNOLOGY LEADER</p>
        <p class="text-muted">Product leader seeking the next opportunity to align teams, drive strategy, and deliver data-informed results.</p>

        <div class="d-flex justify-content-center flex-wrap gap-2 pt-3">
            <a href="https://www.linkedin.com/in/markahansen/" target="_blank" class="btn btn-primary">Mark's LinkedIn</a>
            <a class="btn btn-secondary" href={resume} target="_blank">Mark's Resume</a>
        </div>
    </section>

    <section class="row g-4 mb-5">
        <div class="col-md-6">
            <div class="card h-100">
                <div class="card-body">
                    <h5 class="card-title">💡 Key Features</h5>
                    <ul class="list-unstyled">
                        <li>✔ Product Management</li>
                        <li>✔ Go-to-Market (GTM)</li>
                        <li>✔ Product-Led Growth (PLG)</li>
                        <li>✔ Cross-Functional Leadership</li>
                        <li>✔ Pricing & Packaging</li>
                    </ul>
                </div>
            </div>
        </div>
        <div class="col-md-6">
            <div class="card h-100">
                <div class="card-body">
                    <h5 class="card-title">📈 Latest Metrics & KPIs</h5>
                    <ul class="list-unstyled">
                        <li>👀 53 LinkedIn Profile views in past 30 days</li>
                        <li>📬 4 recruiter conversations</li>
                        <li>✅ 0 interviews in progress</li>
                    </ul>
                </div>
            </div>
        </div>
    </section>
    <section class="mb-5">
        <div class="card">
            <div class="card-body">
                <h5 class="card-title">📰 {title}</h5>
                <h6 class="card-subtitle mb-2 text-muted">{postDate}</h6>
                <p>{@html postContent}</p>
            </div>
        </div>
    </section>

    <Stats />

    <section class="mb-5">
        <div class="card">
            <div class="card-body">
                <h5 class="card-title">📝 Previous Updates</h5>
                <ul class="list-unstyled">
                    {#each allPosts as Post}
                        <li>v{new Date(Post.cardDate).getFullYear()}.{Post.postid} - <a href="javascript:void(0)" on:click={() => changePost(Post.postid)}>{Post.cardTitle}</a></li>
                    {/each}
                </ul>
            </div>
        </div>
    </section>

        <!--
        <section class="mb-5">
            <div class="card">
                <div class="card-body">
                    <h5 class="card-title">💬 Testimonials</h5>
                    <blockquote class="blockquote">
                        <p>“He is just as eager to jump on a customer call to help sales close a deal as he is to help the engineering team work through a complex feature implementation. ”</p>
                    </blockquote>
                    <blockquote class="blockquote">
                        <p>“I've had the pleasure of working with Mark for close to 8 years, and he's not only a fantastic Product professional but also a truly great person. He'll be an invaluable addition to any organization!”</p>
                    </blockquote>
                </div>
            </div>
        </section>
-->
        <section class="text-center">
            <p class="text-muted">Looking to build something meaningful? Let's connect.</p>
        </section>
</main>
