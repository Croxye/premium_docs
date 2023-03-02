# Error Alert Animation

Now that we have everything working, I want to make the error handling a little nicer. Instead of using the standard `alert()` function, I want to use a Tailwind CSS animation and custom error box to show the error message. Let's create a new function called `showError()`.

```js
function showError(msg) {
  errMsg.style.transform = 'translateY(-450px) translateX(-50%)';
  errMsg.innerText = msg;

  setTimeout(() => {
    errMsg.style.transform = 'translateY(-1000px) translateX(-50%)';
  }, 3000);
}
```

We had already created the error box using Tailwind. We just set the `transform` property to move the box up out of view. Now we are setting the `transform` property to move the box back into view and we are setting the `innerText` property to the error message. We are also using the `setTimeout()` function to move the box back out of view after 3 seconds.

We want to call this function in the event handler if the user forgets to pass in a value and also in the `calculateResults()` function if the user enters invalid numbers.

```js
function onLoanFormSubmit(e) {
  e.preventDefault();

  resetUI();

  // Validate input
  if (
    amountInput.value === '' ||
    interestInput.value === '' ||
    yearsInput.value === ''
  ) {
    showError('Please fill in all fields!'); // <------ ADD THIS LINE
    return;
  }

  const principal = parseFloat(amountInput.value);
  const monthlyInterest = parseFloat(interestInput.value) / 100 / 12;
  const numberOfPayments = parseFloat(yearsInput.value) * 12;

  calculateResults(principal, monthlyInterest, numberOfPayments);
}
```

```js
function calculateResults(principal, monthlyInterest, numberOfPayments) {
  const x = Math.pow(1 + monthlyInterest, numberOfPayments);
  // Get monthly payment
  const monthly = ((principal * x * monthlyInterest) / (x - 1)).toFixed(2);
  // Get total payment
  const total = (monthly * numberOfPayments).toFixed(2);
  // Get total interest
  const interest = (monthly * numberOfPayments - principal).toFixed(2);

  // console.log(monthly, total, interest);

  if (isNaN(monthly)) {
    showError('Please check your numbers'); // <------ ADD THIS LINE
    return;
  } else {
    addResultsToDOM(monthly, total, interest);
  }
}
```
