<script>
    import { stores } from '@sapper/app';

    const { page, session } = stores();
    let literature = '';
</script>
<div class="six">
    <div class="three container">
        <div class="ten">
            <a rel='prefetch' class:active="{$page.path === '/japanliterature'}" href="/pageliterature"><div class="five"></div></a>
        </div>
        <div class="ten">
            <div class="four">
                <div class="seven" style="text-align: center"><h2 class="bind:value={literature}">Название</h2></div>
                <div class="eight" style="text-align: center"><p class="text-gray-600 mb-2 text-center">Жанр/Категория Жанр/Категория Жанр/Категория</p></div>
                <div class="nine"><p class="leading-normal text-left slide-in-bottom-subtitle">
                    Прошёл год с того момента, как Тору Хонда поселилась в доме семьи Сома. За это время она укрепила отношения с живущими в нём Сигурэ, Кё и Юки. Кроме того, она сблизилась с другими членами семьи и, помогая им с множеством личных проблем, узнала об их родовой тайне. Однако чем больше узнаёт Тору, тем лучше понимает, что этот секрет скрывает правду намного темнее, чем она предполагала сначала.

                    Приближается лето, и Хонду приглашают провести его вместе с Сома, по большей части с Кё и Юки. Тору надеется на спокойные каникулы, однако её близкие отношения с двумя парнями и остальными членами их семьи могут оказаться причиной неприятностей. По мере того, как они становятся ближе, их совместному беззаботному времяпровождению препятствуют старые трудности и чувства из прошлого, начинающие всплывать на поверхность.

                    Традиционный Банкет не за горами, и все члены «зодиака» должны выполнять свои обязанности бок о бок с нервным главой семьи, Акито. С приближением Банкета и избытком чувств, в которых нужно разобраться, останется ли жизнь Тору с семьёй Сома такой же мирной, или же она окажется в ситуации, из которой выхода нет?
                    Автор:WardiggerWardigger
                </p>
                </div>
            </div>
        </div>
    </div>
</div>
<style>

    .three
    {
        flex-1: auto;
        background-color: #e2e8f0;
        box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
        border: black;
        border-radius: 2px;
        border: 1px solid #aaa;
        padding: 4px;
    }
    .four
    {
        background-color: #f7fafc;
        padding:20px;
        border: 1px solid #000;
        border-radius: 4px;
        font-family: 'Roboto', sans-serif;
    }
    .five
    {
        background-color: #718096;
        width: auto;
        height: 256px;
        border: 1px solid #000;
        border-radius: 4px;
        font-family: 'Roboto', sans-serif;
    }
    .six
    {
        padding: 4px;
    }
    .seven
    {
        color: blue;
        font-weight: bold;
        align-items: center;
        font-family: 'Roboto', sans-serif;
    }
    .seven h2
    {
        color: blue;
    }
    .eight
    {
        font-weight: bold;
        font-family: 'Roboto', sans-serif;
    }
    .nine
    {
        font-family: 'Roboto', sans-serif;
    }
    .ten
    {
        padding:20px;
    }
</style>
