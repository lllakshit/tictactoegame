# tictactoegame
<!-- html code here -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="s.css">
</head>
<body>
<div class="msg-container hide">
    <p id="msg"> Winner </p>
    <button id="new-btn"> New Game</button>
</div>
<main> 
    <h1>tic tac toe game </h1>
    <div class="container">
        <div class="game">
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
            <button class="box"></button>
        </div>
    </div>
    <button id="reset-btn">Reset Button</button>
</main>

<script src="s.js"></script>
</body>
</html>
<!-- Css code is here -->
*{
    margin: 0;
    padding: 0;
}
body{
    background-color: #548587 ;
    text-align: center;
}
.container{
    height: 70vh;
    display: flex;
    justify-content: center;
    align-items: center;
    gap:1.5rem vmin;

}
.game{
    height: 60vmin;
    width: 60vmin;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap:1.5rem vmin;
}
.box{
    height: 18vmin;
    width:18vmin;
    border-radius: 1rem;
    border: none;
    gap: 1.5%rem;
    box-shadow: 0 0 1rem rgba(0,0,0,0.3);
    font-size: 8vmin;
    color: #b0413e;
    background-color: #ffffc7;
}
#reset-btn {
    padding: 1rem;
    font-size: 1.25rem;
    background-color:#191913 ;
    color: #fff;
    border-radius: 1rem;
    border: none;
}
#new-btn{
    padding: 1rem;
    font-size: 1.25rem;
    background-color:#191913 ;
    color: #fff;
    border-radius: 1rem;
    border: none;
}
#msg{
    color: #ffffc7;
    font-size: 5vmin;
}
.msg-container{
   height: 100vmin;
   display: flex;
   flex-wrap: wrap;
   justify-content: center;
   align-items: center;
   flex-direction: column;
   gap: 4rem;
}
.hide{
    display: none;
}
<!-- js code is here -->
let boxes = document.querySelectorAll(".box");
let resetBtn = document.querySelector(".reset-btn");
let newGameBtn = document.querySelector("#new-btn");
let msgContainer = document.querySelector(".msg-container");
let msg = document.querySelector("#msg");
let turn0 = true; // player x player y
// creating a 2D array 
const resetGame = () => {
    turn0 = true;
    enable();
    msgContainer.classList.add("hide");
    // Clearing the text inside the boxes
    boxes.forEach((box) => {
        box.innerText = "";
    });
};
let arr = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
];

boxes.forEach((box) => {
    box.addEventListener("click", () => {
        console.log("the box has been clicked ");
        if (box.innerText === "") {
            if (turn0 === true) {
                box.innerText = "0";
                turn0 = false;
            } else {
                box.innerText = "X";
                turn0 = true;
            }
            box.disabled = true;
            checkWinner();
        }
    });
});

const disable = () => {
    boxes.forEach((box) => {
        box.disabled = true;
    });
};

const enable = () => {
    boxes.forEach((box) => {
        box.disabled = false;
    });
};

const showWinner = (winner) => {
    disable();
    msg.innerHTML = (winner === "") ? "It's a tie!" : `CONGRATS, THE WINNER IS ${winner}`;
    msgContainer.classList.remove("hide");
};

const checkWinner = () => {
    for (let pattern of arr) {
        let pos1val = boxes[pattern[0]].innerText;
        let pos2val = boxes[pattern[1]].innerText;
        let pos3val = boxes[pattern[2]].innerText;
        if (pos1val !== "" && pos2val !== "" && pos3val !== "") {
            if (pos1val === pos2val && pos2val === pos3val) {
                showWinner(pos1val);
                return;
            }
        }
    }
    // Check for a tie
    let isTie = true;
    for (let box of boxes) {
        if (box.innerText === "") {
            isTie = false;
            break;
        }
    }
    if (isTie) {
        showWinner("");
    }
};

newGameBtn.addEventListener("click", resetGame);
resetBtn.addEventListener("click", resetGame);

