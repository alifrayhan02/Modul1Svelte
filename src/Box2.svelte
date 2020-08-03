<style>
    .box {
        width: 300px;
        border: 2px solid #aaa;
        border-radius: 40px;
        padding: 2rem;
        background: white;
    }
</style>

<div class="box">
    <header>
        <slot name="header" />
    </header>
    <article>
        <span>tidak ada yang ingin ditampilkan :(</span>
    </article>
    <footer>
        <slot name="footer" />
    </footer>
</div>