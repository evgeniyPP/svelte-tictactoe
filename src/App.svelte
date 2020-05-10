<script>
    import Space from './Space.svelte';
    import gameStore from './game.store.js';
    import { nextMove } from './requests.js';

    let board = ['', '', '', '', '', '', '', '', ''];
    let nextPlayer = '';
    let winner;
    let numberOfPeeps = 0;
    let errorMessage;

    gameStore.subscribe(data => {
        if (!data) {
            return;
        }

        winner = data.winner;
        nextPlayer = data.nextPlayer;
        board = data.board;
        numberOfPeeps = data.numberOfPeeps;
    });

    async function takeSpace(space) {
        if (winner || !gameStore.isConnected()) {
            return;
        }

        errorMessage = await nextMove(space);
    }
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
        <Space {winner} space={board[0]} on:click={takeSpace(0)} />
        <Space {winner} space={board[1]} on:click={takeSpace(1)} />
        <Space {winner} space={board[2]} on:click={takeSpace(2)} />
    </div>
    <div class="row">
        <Space {winner} space={board[3]} on:click={takeSpace(3)} />
        <Space {winner} space={board[4]} on:click={takeSpace(4)} />
        <Space {winner} space={board[5]} on:click={takeSpace(5)} />
    </div>
    <div class="row">
        <Space {winner} space={board[6]} on:click={takeSpace(6)} />
        <Space {winner} space={board[7]} on:click={takeSpace(7)} />
        <Space {winner} space={board[8]} on:click={takeSpace(8)} />
    </div>
    {#if winner}
        <button>Новая игра</button>
    {/if}
    {#if errorMessage}
        <p class="errorMessage">{errorMessage}</p>
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

    .errorMessage {
        color: red;
        font-size: 20px;
    }
</style>
