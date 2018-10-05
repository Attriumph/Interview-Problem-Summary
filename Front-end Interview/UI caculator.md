```HTML
<html>
<head>
  <style>
    body {
      background-color: #1d2126;
      color: white;
    }

    #caculator {
      width:300px;
      text-align: center;
      margin: auto;
      border: 1px solid #fff;
      border-radius: 5px;
    }

    #display {
      border: 1px solid #fff;
      border-radius: 5px;
      margin: 5px;
      height: 50px;
      background-color: white;
      text-align: right;
      color: black;

    }

    .operator span {
      display: inline-block;
      width: 50px;
      height: 50px;
      font-size: 50px;
      border: 1px solid #fff;
      border-radius: 3px;
      cursor: pointer;
      margin: 5px;

    }

    #leftPanel {
     display: inline-block;
    }

    .number span {
      display: inline-block;
      width: 50px;
      height: 50px;
      font-size: 50px;
      border: 1px solid #fff;
      border-radius: 3px;
      cursor: pointer;
      margin: 5px;

    }

    #equal {

      display: inline-block;
      width: 50px;
      height: 220px;
      font-size: 50px;
      border: 1px solid #fff;
      border-radius: 3px;
      cursor: pointer;
      background-color: #ddd;
      margin-top: 5px;
      vertical-align: top;
      color: blue;
    }
  </style>
</head>
<body>
  <div id="caculator">
  <div id="display"></div>
  <div class="operator">
    <span>+</span>
    <span>-</span>
    <span>&times;</span>
    <span>&divide;</span>
  </div>
  <div id="leftPanel">
    <div class="number">
      <span>1</span>
      <span>2</span>
      <span>3</span>
    </div>
    <div class="number">
      <span>4</span>
      <span>5</span>
      <span>6</span>
    </div>
    <div class="number">
      <span>7</span>
      <span>8</span>
      <span>9</span>
    </div>
    <div class="number">
      <span>0</span>
      <span>.</span>
      <span id="clear">C</span>
    </div>
 </div>

 <div id="equal">=</div>

</div>
 <script>
   // let  operations = {
   // "÷": (a,b)=> a/b;
   // "×": (a,b)=> a*b;
   // "-": (a,b)=> a-b;
   // "+": (a,b)=> parseFloat(a)+parseFloat(b);
   // };

   let operations = {
"÷": function(a,b) { return a/b;},
"×": function(a,b) { return a*b;},
"-": function(a,b) { return a-b;},
// using parseFloat is necessary, otherwise it will result in string concatenation
"+": function(a,b) { return parseFloat(a)+parseFloat(b);}
};

   let operationChars = Object.keys(operations);
   let display = document.getElementById("display");
   let numbers = document.querySelectorAll(".number span");
   let operators = document.querySelectorAll(".operator span");
   let clear = document.getElementById("clear");
   let result = document.getElementById("equal");
   let resultDisplay = false;
   console.log(display);
   console.log(numbers);
   console.log(operators);
   console.log(result);



   for (let i = 0; i < numbers.length; i++) {
    numbers[i].addEventListener("click", function(e) {
    console.log("click number");
    let currentString = display.innerHTML;
    let lastChar = currentString[currentString.length - 1];


    if (resultDisplay === false) {
      display.innerHTML += e.target.innerHTML;

    } else if (resultDisplay === true && operationChars.indexOf(lastChar) >= 0) {

    resultDisplay = false;
    display.innerHTML += e.target.innerHTML;

   } else {

    resultDisplay = false;
    display.innerHTML = e.target.innerHTML;
  }

   });
  }


   for (let i = 0; i < operators.length; i++) {
    operators[i].addEventListener("click", function(e) {

    let currentString = display.innerHTML;

    if (currentString.length !== 0) {
      display.innerHTML += e.target.innerHTML;
    }
   });
  }


   result.addEventListener("click", function() {
      console.log(operationChars);
      let inputString = display.innerHTML;
      let numbers = inputString.split(/\+|\-|\÷|\×/g);
      let myOperators = inputString.replace(/[0-9]|\./g,"").split("");

     //  console.log(numbers);
     console.log(myOperators);


      for (let i = 0; i < operationChars.length; i++) {
        let currentOperator = operationChars[i];
        // console.log(operations);
        let currentOperation = operations[currentOperator];
        // console.log(currentOperation);
        let nextOperationToExecute = myOperators.indexOf(currentOperator);
             console.log(nextOperationToExecute);

        while (nextOperationToExecute !== -1) {
          let nextResult = currentOperation(numbers[nextOperationToExecute], numbers[nextOperationToExecute + 1]);
          numbers.splice(nextOperationToExecute, 2, nextResult);
          myOperators.splice(nextOperationToExecute, 1);
           nextOperationToExecute = myOperators.indexOf(currentOperator);
  }
}
display.innerHTML = numbers[0];
resultDisplay = true;
   });


   clear.addEventListener("click", function() {
     display.innerHTML = "";
   });

 </script>   
</body>
</html>
```
<html>
<head>
  <style>
    body {
      background-color: #1d2126;
      color: white;
    }

    #caculator {
      width:300px;
      text-align: center;
      margin: auto;
      border: 1px solid #fff;
      border-radius: 5px;
    }

    #display {
      border: 1px solid #fff;
      border-radius: 5px;
      margin: 5px;
      height: 50px;
      background-color: white;
      text-align: right;
      color: black;

    }

    .operator span {
      display: inline-block;
      width: 50px;
      height: 50px;
      font-size: 50px;
      border: 1px solid #fff;
      border-radius: 3px;
      cursor: pointer;
      margin: 5px;

    }

    #leftPanel {
     display: inline-block;
    }

    .number span {
      display: inline-block;
      width: 50px;
      height: 50px;
      font-size: 50px;
      border: 1px solid #fff;
      border-radius: 3px;
      cursor: pointer;
      margin: 5px;

    }

    #equal {

      display: inline-block;
      width: 50px;
      height: 220px;
      font-size: 50px;
      border: 1px solid #fff;
      border-radius: 3px;
      cursor: pointer;
      background-color: #ddd;
      margin-top: 5px;
      vertical-align: top;
      color: blue;
    }
  </style>
</head>
<body>
  <div id="caculator">
  <div id="display"></div>
  <div class="operator">
    <span>+</span>
    <span>-</span>
    <span>&times;</span>
    <span>&divide;</span>
  </div>
  <div id="leftPanel">
    <div class="number">
      <span>1</span>
      <span>2</span>
      <span>3</span>
    </div>
    <div class="number">
      <span>4</span>
      <span>5</span>
      <span>6</span>
    </div>
    <div class="number">
      <span>7</span>
      <span>8</span>
      <span>9</span>
    </div>
    <div class="number">
      <span>0</span>
      <span>.</span>
      <span id="clear">C</span>
    </div>
 </div>

 <div id="equal">=</div>

</div>
 <script>
   // let  operations = {
   // "÷": (a,b)=> a/b;
   // "×": (a,b)=> a*b;
   // "-": (a,b)=> a-b;
   // "+": (a,b)=> parseFloat(a)+parseFloat(b);
   // };

   let operations = {
"÷": function(a,b) { return a/b;},
"×": function(a,b) { return a*b;},
"-": function(a,b) { return a-b;},
// using parseFloat is necessary, otherwise it will result in string concatenation
"+": function(a,b) { return parseFloat(a)+parseFloat(b);}
};

   let operationChars = Object.keys(operations);
   let display = document.getElementById("display");
   let numbers = document.querySelectorAll(".number span");
   let operators = document.querySelectorAll(".operator span");
   let clear = document.getElementById("clear");
   let result = document.getElementById("equal");
   let resultDisplay = false;
   console.log(display);
   console.log(numbers);
   console.log(operators);
   console.log(result);



   for (let i = 0; i < numbers.length; i++) {
    numbers[i].addEventListener("click", function(e) {
    console.log("click number");
    let currentString = display.innerHTML;
    let lastChar = currentString[currentString.length - 1];


    if (resultDisplay === false) {
      display.innerHTML += e.target.innerHTML;

    } else if (resultDisplay === true && operationChars.indexOf(lastChar) >= 0) {

    resultDisplay = false;
    display.innerHTML += e.target.innerHTML;

   } else {

    resultDisplay = false;
    display.innerHTML = e.target.innerHTML;
  }

   });
  }


   for (let i = 0; i < operators.length; i++) {
    operators[i].addEventListener("click", function(e) {

    let currentString = display.innerHTML;

    if (currentString.length !== 0) {
      display.innerHTML += e.target.innerHTML;
    }
   });
  }


   result.addEventListener("click", function() {
      console.log(operationChars);
      let inputString = display.innerHTML;
      let numbers = inputString.split(/\+|\-|\÷|\×/g);
      let myOperators = inputString.replace(/[0-9]|\./g,"").split("");

     //  console.log(numbers);
     console.log(myOperators);


      for (let i = 0; i < operationChars.length; i++) {
        let currentOperator = operationChars[i];
        // console.log(operations);
        let currentOperation = operations[currentOperator];
        // console.log(currentOperation);
        let nextOperationToExecute = myOperators.indexOf(currentOperator);
             console.log(nextOperationToExecute);

        while (nextOperationToExecute !== -1) {
          let nextResult = currentOperation(numbers[nextOperationToExecute], numbers[nextOperationToExecute + 1]);
          numbers.splice(nextOperationToExecute, 2, nextResult);
          myOperators.splice(nextOperationToExecute, 1);
           nextOperationToExecute = myOperators.indexOf(currentOperator);
  }
}
display.innerHTML = numbers[0];
resultDisplay = true;
   });


   clear.addEventListener("click", function() {
     display.innerHTML = "";
   });

 </script>   
</body>
</html>
