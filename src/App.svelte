<script>
    import Space from './Space.svelte';
    import gameStore from './game.store.js';

    let board = ['', '', '', '', '', '', '', '', ''];
    let nextPlayer = '';
    let winner;
    let numberOfPeeps = 0;

    gameStore.subscribe(data => {
        if (!data) {
            return;
        }

        winner = data.winner;
        nextPlayer = data.nextPlayer;
        board = data.board;
        numberOfPeeps = data.numberOfPeeps;
    });
</script>

<main>
    <h1>Крестики-нолики</h1>
    <h2>Количество игроков: {numberOfPeeps}</h2>
    {#if winner === 'TIE'}
        <h2>Ничья</h2>
    {:else if winner}
        <h2>{winner} победил!</h2>
    {:else}
        <h2>Ходит игрок {nextPlayer}</h2>
    {/if}

    <div class="row">
        <Space space={board[0]} />
        <Space space={board[1]} />
        <Space space={board[2]} />
    </div>
    <div class="row">
        <Space space={board[3]} />
        <Space space={board[4]} />
        <Space space={board[5]} />
    </div>
    <div class="row">
        <Space space={board[6]} />
        <Space space={board[7]} />
        <Space space={board[8]} />
    </div>
    {#if winner}
        <button>Новая игра</button>
    {/if}
</main>

<style>
    main {
        width: 475px;
        margin: 0 auto;
        height: 1000px;
    }

    .row {
        display: flex;
    }

    button {
        width: 100%;
        margin-top: 20px;
        background-color: #26a69a;
        color: white;
        font-size: 24px;
        cursor: pointer;
        padding: 1rem;
        border: none;
        border-radius: 2px;
        box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14),
            0 3px 1px -2px rgba(0, 0, 0, 0.12), 0 1px 5px 0 rgba(0, 0, 0, 0.2);
        transition: 0.3s ease-out;
    }

    button:hover {
        outline: none;
        background-color: #1d6860;
        transition: 0.3s ease-out;
    }

    button:active {
        background-color: #26a69a;
    }
</style>
