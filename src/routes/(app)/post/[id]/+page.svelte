<script>    
    import Layout from "$lib/components/Layout.svelte"
    import Video from "$lib/components/Video.svelte"
    let { data } = $props()
    let post = $state(data.post)
    const Categories = {
        news: 'ព័ត៌មាន',
        national: 'ក្នុង​ប្រទេស',
        global: "ក្រៅ​ប្រទេស",
        opinion: "មតិយោបល់",
        doc: "ឯកសារ",
        sport: "កីឡា",
        movie: 'ភាពយន្ត',
        Khmer: 'រឿងខ្មែរ',
        Thai: 'រឿងថៃ',
        Chinese: 'រឿងចិន',
        Korean: 'រឿងកូរ៉េ',
        world: 'រឿង​​បរទេស',
        travel: 'ដើរ​លេង',
        game: 'ពិភព​និម្មិត',
        template: 'គំរូ​គេហទំព័រ',
    }

    let postCategories = $state(data.post.categories.split(","))
    let categories = $state(postCategories.map((category)=>Categories[category.trim()]))

</script>

<Layout {data}>
<section class="Post region">
    <div class="main">
        <h3 class="title">{post.title}</h3>
        <div class="categories">
            <span>​​​​​​​​​ជំពូកៈ {(categories.filter(Boolean)).join(', ')}</span>
            <span>{(new Date(post.date)).toLocaleDateString('it-IT')}</span>
        </div>
        <div class="author">
            <span>​​​​​​​​​​ចុះ​ផ្សាយ​ដោយៈ {data.authorName}</span>
        </div>
        {#if post.videos.length > 0}
            <Video {data} />
        {/if}
        <div class="content">
            {@html post.content}
        </div>
        <div class='post-bottom'>
            <div class="social-media">
                <span class="fb-share-button" data-href={`https://khmerweb-news.netlify.app/post/${post.id}`} data-layout="" data-size=""><a target="_blank" href={`https://www.facebook.com/sharer/sharer.php?u=https://khmerweb-news.netlify.app/post/${post.id}%2F&amp;src=sdkpreparse`} class="fb-xfbml-parse-ignore">Share</a></span>
            </div>
            {#if data.user}
            <div class='edit'>
                <a href={`/admin/post/edit/${post.id}`}><img src="/images/edit.png" alt=''/></a>
                <a href={`/admin/post/delete/${post.id}`}><img src="/images/delete.png" alt=''/></a>
            </div>
            {/if}
        </div>
        <div class="fb-comments" data-href={`https://khmerweb-news.netlify.app/post/${post.id}`} data-width="100%" data-numposts="5"></div>
    </div>
    <div class="sidebar">
        {#each data.randomPosts as post}
            <a  href={`/post/${post._id.$oid}`}>
                <img src={post.thumb} alt=''/>
                {#if post.videos.length}
                <img class="play-icon" src="/images/play.png" alt=''/>
                {/if}
                <div class="title">{post.title}</div>
            </a>
        {/each}
    </div>

</section>
</Layout>

<style>
.Post{
    margin-top: 15px;
    display: grid;
    grid-template-columns: 70% auto;
    grid-gap: 15px;
    padding-bottom: 30px;
}
.Post .main{
    background-color: lightblue;
    color: rgb(22, 22, 22);
    padding: 15px;
}
.Post .main .title{
    font: 18px/1.5 Oswald, Koulen;
    margin-bottom: 20px;
}
.Post .main .categories span:nth-child(2){
    float: right;
}
.Post .main .author{
    padding-bottom: 0px;
}
.Post .main .content{
    margin: 20px 0;
    font: 14px/1.5 Courgette, Nokora;
    text-align: center;
}
:global(.Post .main .content img){
    width: 100%;
}
:global(.Post .main .content a){
    width: 25%;
    background: var(--background);
    color: white;
    font: var(--body-font);
    font-size: 16px;
    padding: 3px 10px;
    margin: 0 5px;
}
.Post .sidebar a{
    display: block;
    color: white;
    position: relative;
    padding-top: 56.25%;
    overflow: hidden;
    margin-bottom: 15px;
}
.Post .sidebar a:last-child{
    margin-bottom: 0;
}
.Post .sidebar a img{
    position: absolute;
    width: 100%;
    min-height: 100%;
    top: 0;
    left: 0;
}
.Post .sidebar a .play-icon{
    width: auto;
    min-height: auto;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    width: 15%;
}
.Post .sidebar a .title{
    position: absolute;
    bottom: 0;
    padding: 5px 10px;
    font: 16px/1.5 Oswald, Bayon;
    text-shadow: 2px 2px 4px #000000;
    background: -webkit-linear-gradient(bottom, black,transparent);
    width: 100%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
.Post .main .post-bottom{
    display: grid;
    grid-template-columns: auto auto;
}
.Post .main .post-bottom .edit{
    text-align: right; 
}
.Post .main .post-bottom .edit img{
    width: 30px;
}
.Post .main .social-media{
    width: 50px;
    display: grid;
    grid-template-columns: auto auto;
    grid-gap: 5px;
    align-items: center;
}

@media only screen and (max-width:600px){
    .Post{
        grid-template-columns: 100%;
    }
    .Post .sidebar{
        padding: 0 15px;
    }
}
</style>