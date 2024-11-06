<script>
    let { data } = $props()
    const featured = data.posts
    function navigate(event){
        document.location=event.target.value
    }
</script>

<section class="latest">
    <div class="panel">
        {#each featured as post}
            <div>
                <a class="title" href={`/post/${post.id}`}>{post.title}</a>
                <a class="thumb" href={`/post/${post.id}`}>
                    <img src={post.thumb} alt='' />
                </a>
            </div>
        {/each}
    </div>
    {#if data.pageNumber>=1 }
    <div class="pagination">
        <span>​​​​​​​​​​​​​​​​​​​​​ទំព័រ</span> 
        <select onchange={navigate}> 
        {#each [...Array(data.pageNumber).keys()] as page}
            {#if page+1 == parseInt(data.navPage) }
                <option selected>{page+1}</option>
            {:else}
                <option>{page+1}</option>
            {/if}            
        {/each}	
        </select> 
        <span>នៃ {data.pageNumber}</span>
    </div>
    {/if}
</section>

<style>
.latest .panel{
    display: grid;
    grid-template-columns: repeat(3, calc(100% / 3 - 13.33px));
    grid-gap: 40px 20px;
    padding-top: 20px;
}
.latest .panel .thumb{
    position: relative;
    padding-top: 100%;
    overflow: hidden;
    width: 100%;
    display: block;
}
.latest .panel .thumb img{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
}
.latest .panel .title{
    padding: 5px 10px;
    text-align: center;
    font: 16px/1.5 Oswald, Bayon;
    color: white;
    background: var(--link);
    width: 100%;
    display: block;
}
.latest .pagination{
    text-align: center;
    padding: 20px;
}
.latest .pagination > span{
    padding: 0 5px;
}

@media only screen and (max-width: 600px){
    .latest .panel{
        grid-template-columns: 100%;
        padding: 10px 10px 0;
    }   
}
</style>