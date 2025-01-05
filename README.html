<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tetris Game</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #282c34;
            color: #ffffff;
            font-family: Arial, sans-serif;
        }
        #tetris-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            position: relative;
        }
        #hold-container, #next-container {
            margin-bottom: 20px;
        }
        #hold, #next {
            background-color: #1e1e1e;
            border: 4px solid #61dafb;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
        }
        canvas {
            background-color: #1e1e1e;
            border: 4px solid #61dafb;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
            display: block;
        }
        .controls {
            margin-top: 20px;
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .control-buttons-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        .control-buttons.vertical {
            flex-direction: column;
        }
        .control-buttons.horizontal {
            display: flex;
            flex-direction: row;
        }
        .score {
            margin-bottom: 20px;
            font-size: 24px;
        }
        button {
            margin: 5px;
            padding: 15px 20px;
            font-size: 18px;
            font-weight: bold;
            color: #282c34;
            background-color: #61dafb;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #4fb1e8;
        }
        button:active {
            background-color: #3a93c7;
        }
        #comments {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            overflow: hidden;
        }
        .comment {
            position: absolute;
            white-space: nowrap;
            font-size: 24px;
            color: #fff;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
            animation: slideLeft 10s linear infinite;
        }
        @keyframes slideLeft {
            from {
                transform: translateX(100%);
            }
            to {
                transform: translateX(-100%);
            }
        }
        @media (max-width: 600px) {
            canvas {
                width: 240px;
                height: 480px;
            }
            button {
                padding: 10px 15px;
                font-size: 16px;
            }
        }
    </style>
</head>
<body>
    <div id="tetris-container">
        <div id="hold-container">
            <canvas id="hold" width="80" height="80"></canvas>
        </div>
        <div id="next-container">
            <canvas id="next" width="80" height="80"></canvas>
        </div>
        <div class="score" id="score">Score: 0</div>
        <canvas id="tetris" width="200" height="400"></canvas>
        <div id="comments"></div>
        <div class="controls">
            <div class="control-buttons-container">
                <button id="hold-button">Hold</button>
                <div class="control-buttons horizontal">
                    <button id="left-button">Left</button>
                    <button id="rotate-button">Rotate</button>
                    <button id="right-button">Right</button>
                </div>
                <button id="drop-button" onmousedown="startDrop()" onmouseup="stopDrop()">Drop</button>
            </div>
        </div>
    </div>
    <script>
        const canvas = document.getElementById('tetris');
        const context = canvas.getContext('2d');
        context.scale(20, 20);

        const holdCanvas = document.getElementById('hold');
        const holdContext = holdCanvas.getContext('2d');
        holdContext.scale(10, 10);

        const nextCanvas = document.getElementById('next');
        const nextContext = nextCanvas.getContext('2d');
        nextContext.scale(10, 10);

        // 効果音ファイルの読み込み
        const moveSound = new Audio('move.mp3'); // 横移動時の効果音
        const dropSound = new Audio('drop.mp3'); // ブロックが落ちるときの効果音
        const lineClearSound = new Audio('line-clear.mp3'); // ラインが消えるときの効果音
        const rotateSound = new Audio('rotate.mp3'); // 回転時の効果音
        const holdSound = new Audio('hold.mp3'); // ホールド時の効果音

        let dropInterval = 1000;
        let dropCounter = 0;
        let dropTimer;
        let moveInterval;
        let holdPiece = null;
        let holdUsed = false;
        let nextPiece = null;
        let pieceBag = [];

        function arenaSweep() {
            let rowCount = 1;
            outer: for (let y = arena.length - 1; y > 0; --y) {
                for (let x = 0; x < arena[y].length; ++x) {
                    if (arena[y][x] === 0) {
                        continue outer;
                    }
                }
                const row = arena.splice(y, 1)[0].fill(0);
                arena.unshift(row);
                ++y;
                player.score += rowCount * 10;
                rowCount *= 2;
                lineClearSound.play(); // ラインが消えたときの効果音
                addComment("Nice clear!");
            }
            updateScore();
        }

        function updateScore() {
            document.getElementById('score').innerText = 'Score: ' + player.score;
        }

        function collide(arena, player) {
            const [m, o] = [player.matrix, player.pos];
            for (let y = 0; y < m.length; ++y) {
                for (let x = 0; x < m[y].length; ++x) {
                    if (m[y][x] !== 0 &&
                       (arena[y + o.y] &&
                        arena[y + o.y][x + o.x]) !== 0) {
                        return true;
                    }
                }
            }
            return false;
        }

        function createMatrix(w, h) {
            const matrix = [];
            while (h--) {
                matrix.push(new Array(w).fill(0));
            }
            return matrix;
        }

        function createPiece(type) {
            switch (type) {
                case 'T':
                    return [
                        [0, 0, 0],
                        [1, 1, 1],
                        [0, 1, 0],
                    ];
                case 'O':
                    return [
                        [2, 2],
                        [2, 2],
                    ];
                case 'L':
                    return [
                        [0, 3, 0],
                        [0, 3, 0],
                        [0, 3, 3],
                    ];
                case 'J':
                    return [
                        [0, 4, 0],
                        [0, 4, 0],
                        [4, 4, 0],
                    ];
                case 'I':
                    return [
                        [0, 5, 0, 0],
                        [0, 5, 0, 0],
                        [0, 5, 0, 0],
                        [0, 5, 0, 0],
                    ];
                case 'S':
                    return [
                        [0, 6, 6],
                        [6, 6, 0],
                        [0, 0, 0],
                    ];
                case 'Z':
                    return [
                        [7, 7, 0],
                        [0, 7, 7],
                        [0, 0, 0],
                    ];
            }
        }

        function drawGrid() {
            context.lineWidth = 0.05;
            context.strokeStyle = '#444';
            for (let x = 0; x < canvas.width / 20; x++) {
                context.beginPath();
                context.moveTo(x, 0);
                context.lineTo(x, canvas.height / 20);
                context.stroke();
            }
            for (let y = 0; y < canvas.height / 20; y++) {
                context.beginPath();
                context.moveTo(0, y);
                context.lineTo(canvas.width / 20, y);
                context.stroke();
            }
        }

        function drawMatrix(matrix, offset, ctx = context) {
            const colors = [
                null,
                '#FF0D72', // T
                '#0DC2FF', // O
                '#0DFF72', // L
                '#F538FF', // J
                '#FF8E0D', // I
                '#FFE138', // S
                '#3877FF'  // Z
            ];
            matrix.forEach((row, y) => {
                row.forEach((value, x) => {
                    if (value !== 0) {
                        ctx.fillStyle = colors[value];
                        ctx.fillRect(x + offset.x, y + offset.y, 1, 1);
                        ctx.strokeStyle = '#000';
                        ctx.lineWidth = 0.1;
                        ctx.strokeRect(x + offset.x, y + offset.y, 1, 1);
                    }
                });
            });
        }

        function draw() {
            context.fillStyle = '#000';
            context.fillRect(0, 0, canvas.width, canvas.height);
            drawGrid();
            drawMatrix(arena, {x: 0, y: 0});
            drawMatrix(player.matrix, player.pos);
            drawHoldPiece();
            drawNextPiece();
        }

        function drawHoldPiece() {
            holdContext.clearRect(0, 0, holdCanvas.width, holdCanvas.height);
            if (holdPiece !== null) {
                drawMatrix(holdPiece, {x: 1, y: 1}, holdContext);
            }
        }

        function drawNextPiece() {
            nextContext.clearRect(0, 0, nextCanvas.width, nextCanvas.height);
            if (nextPiece !== null) {
                drawMatrix(nextPiece, {x: 1, y: 1}, nextContext);
            }
        }

        function merge(arena, player) {
            player.matrix.forEach((row, y) => {
                row.forEach((value, x) => {
                    if (value !== 0) {
                        arena[y + player.pos.y][x + player.pos.x] = value;
                    }
                });
            });
        }

        function rotate(matrix, dir) {
            for (let y = 0; y < matrix.length; ++y) {
                for (let x = 0; x < y; ++x) {
                    [
                        matrix[x][y],
                        matrix[y][x],
                    ] = [
                        matrix[y][x],
                        matrix[x][y],
                    ];
                }
            }
            if (dir > 0) {
                matrix.forEach(row => row.reverse());
            } else {
                matrix.reverse();
            }
        }

        function playerDrop() {
            player.pos.y++;
            if (collide(arena, player)) {
                player.pos.y--;
                merge(arena, player);
                playerReset();
                arenaSweep();
                dropSound.play(); // ブロックが落ちたときの効果音
                addComment("Great drop!");
            }
            dropCounter = 0;
        }

        function playerMove(offset) {
            player.pos.x += offset;
            if (collide(arena, player)) {
                player.pos.x -= offset;
            } else {
                moveSound.play(); // 横移動時の効果音
            }
        }

        function shuffle(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }

        function playerReset() {
            if (pieceBag.length === 0) {
                pieceBag = 'TJLOSZI'.split('');
                shuffle(pieceBag);
            }
            player.matrix = createPiece(pieceBag.pop());
            player.pos.y = 0;
            player.pos.x = (arena[0].length / 2 | 0) -
                           (player.matrix[0].length / 2 | 0);

            if (pieceBag.length === 0) {
                pieceBag = 'TJLOSZI'.split('');
                shuffle(pieceBag);
            }
            nextPiece = createPiece(pieceBag[pieceBag.length - 1]);

            if (collide(arena, player)) {
                arena.forEach(row => row.fill(0));
                player.score = 0;
                updateScore();
                addComment("Game Over!");
            }
            holdUsed = false;
        }

        function rotatePlayer() {
            const pos = player.pos.x;
            let offset = 1;
            rotate(player.matrix, 1);
            while (collide(arena, player)) {
                player.pos.x += offset;
                offset = -(offset + (offset > 0 ? 1 : -1));
                if (offset > player.matrix[0].length) {
                    rotate(player.matrix, -1);
                    player.pos.x = pos;
                    return;
                }
            }
            rotateSound.play(); // 回転時の効果音
        }

        function moveLeft() {
            playerMove(-1);
        }

        function moveRight() {
            playerMove(1);
        }

        function drop() {
            playerDrop();
        }

        function startDrop() {
            drop();
            dropTimer = setInterval(playerDrop, 100);
        }

        function stopDrop() {
            clearInterval(dropTimer);
        }

        function holdPieceFunction() {
            if (!holdUsed) {
                holdSound.play(); // ホールド時の効果音
                if (holdPiece === null) {
                    holdPiece = player.matrix;
                    playerReset();
                } else {
                    let temp = player.matrix;
                    player.matrix = holdPiece;
                    holdPiece = temp;
                    player.pos.y = 0;
                    player.pos.x = (arena[0].length / 2 | 0) -
                                   (player.matrix[0].length / 2 | 0);
                }
                holdUsed = true;
                addComment("Hold! Nice strategy!");
            }
        }

        function addComment(text) {
            const comment = document.createElement('div');
            comment.className = 'comment';
            comment.innerText = text;
            comment.style.top = Math.random() * 80 + '%';
            comment.style.color = `hsl(${Math.random() * 360}, 100%, 50%)`;
            document.getElementById('comments').appendChild(comment);

            setTimeout(() => {
                comment.remove();
            }, 10000);
        }

        let lastTime = 0;
        function update(time = 0) {
            const deltaTime = time - lastTime;
            lastTime = time;

            dropCounter += deltaTime;
            if (dropCounter > dropInterval) {
                playerDrop();
            }

            draw();
            requestAnimationFrame(update);
        }

        const arena = createMatrix(10, 20);

        const player = {
            pos: {x: 0, y: 0},
            matrix: null,
            score: 0,
        };

        playerReset();
        update();
        updateScore();

        document.getElementById('left-button').addEventListener('mousedown', () => {
            moveLeft();
            moveInterval = setInterval(moveLeft, 150);
        });
        document.getElementById('left-button').addEventListener('mouseup', () => {
            clearInterval(moveInterval);
        });

        document.getElementById('right-button').addEventListener('mousedown', () => {
            moveRight();
            moveInterval = setInterval(moveRight, 150);
        });
        document.getElementById('right-button').addEventListener('mouseup', () => {
            clearInterval(moveInterval);
        });

        document.getElementById('rotate-button').addEventListener('click', rotatePlayer);
        document.getElementById('hold-button').addEventListener('click', holdPieceFunction);

        document.addEventListener('keydown', event => {
            if (event.key === 'ArrowLeft') {
                moveLeft();
            } else if (event.key === 'ArrowRight') {
                moveRight();
            } else if (event.key === 'ArrowDown') {
                playerDrop();
            } else if (event.key === ' ') {
                rotatePlayer();
            } else if (event.key === 'c') {
                holdPieceFunction();
            }
        });
    </script>
</body>
</html>
