<script>
    let { data } = $props()
</script>

<link href="/styles/base-backend.css" rel="stylesheet" />
<section class="header">
    <header class='wrapper region'>
        <div class='logo'>
            <a href='/admin'><img src='/images/siteLogo.png' alt='' /></a>
            <a href='/admin'>{data.settings.siteTitle}</a>
        </div>
        <form class='search' action="/admin/search?/search" method="post">
            <select name='category'>
                <option>ទាំងអស់</option>
            </select>
            <input type='text' name='q' placeholder='សរសេរ​ពាក្យ​ត្រូវ​ស្វែងរក...' required />
            <input type='submit' value='ស្វែងរក' /> 
        </form>
        <div class='login'>
            <a href={`/user/${data.user.id}`}>{data.user.name}</a> | <a href="/">ទំព័រ​មុខ</a> | <a href="/admin/logout">ចេញ​ក្រៅ</a>
        </div>
    </header>
    <div class="ribbon"></div>
</section>

<style>
    .header{
        background: var(--background-dark);
    }
    .wrapper{
        display: grid;
        grid-template-columns: auto auto 20%;
        align-items: center;
        padding: 10px 0;
    }
    .wrapper .logo{
        display: grid;
        grid-template-columns: 60px auto;
        align-items: center;
        grid-gap: 10px;
    }
    .wrapper .logo img{
        width: 60px;
    }
    .wrapper .logo a{
        font: 40px/1.5 StardosStencul, Limonf3;
        color: white;
    }
    .wrapper .search{
        display: grid;
        grid-template-columns: 70px auto 15%;
    }
    .wrapper .search input, .wrapper .search select{
        font: var(--body-font);
    }
    .wrapper .search [name='q']{
        padding: 0 5px;
    }
    .wrapper .login{
        text-align: right;
        color: white;
    }
    .wrapper .login a{
        color: white;
    }
    .header .ribbon{
        height: 6px;
        background-color: var(--background);
    }

    @media only screen and (max-width: 600px){
        .wrapper{
            grid-template-columns: 100%;
            padding: 0 10px;
            text-align: center;
        }
        .wrapper .logo{
            grid-template-columns: 100%;
        }
        .wrapper .login{
            text-align: center;
            padding: 10px 0;
        }
    }
</style>