<script>
    import { Link } from 'svelte-routing';
</script>

<style>
    .container {
        position: relative;
    }
</style>

<nav>
    <div class="nav-wrapper">
        <div class="container">
            <div class="brand-logo right">
                <Link to="/">Svelte Tutorial</Link>
            </div>
            <ul id="nav-mobile" class="left">
                <li><Link to="/">Home</Link></li>
                <li><Link to="/about">About</Link></li>
            </ul>
        </div>
    </div>
</nav>