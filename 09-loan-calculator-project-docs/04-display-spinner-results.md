# Display Spinner and Results

Now that we have the results, we need to display them on the page. Let's create a function called `addResultsToDOM()`.

```js
function addResultsToDOM(monthly, total, interest) {
  monthlyResult.innerText = '$' + monthly;
  paymentResult.innerText = '$' + total;
  interestResult.innerText = '$' + interest;
}
```

Now, call the function in the `calculateResults()` function.

```js
function calculateResults(principal, monthlyInterest, numberOfPayments) {
  //...

  if (isNaN(monthly)) {
    alert('Please check your numbers');
    return;
  } else {
    addResultsToDOM(monthly, total, interest);
  }
}
```

This function will put the correct number results where they need to go, but the main `#results` element is still hidden because we have the Tailwind class of `hidden` on it. I want to show a spinner for 1 second and then display the results. So let's create a function called `showSpinnerAndResults()`.

```js
function showSpinnerAndResults(seconds) {
  const spinner = document.getElementById('spinner');
  spinner.style.display = 'block';

  setTimeout(() => {
    spinner.style.display = 'none';
    loanResults.style.display = 'block';
  }, seconds * 1000);
}
```

Here, we are taking in the number of seconds to show the spinner and we are using the `setTimeout()` function to show the spinner for that amount of seconds and then hide it and show the results.

Now, let's call this function in the `addResultsToDOM()` function. You could also call it in the `calculateResults()` function if you want.

```js
function addResultsToDOM(monthly, total, interest) {
  //...

  showSpinnerAndResults(1); // <------ ADD THIS LINE
}
```

At the moment, if we try and use the calculator again, it will still show the results from the previous calculation and the spinner. Let's fix that by adding a `resetUI()` function.

```js
function resetUI() {
  loanResults.style.display = 'none';
  monthlyResult.innerText = '';
  paymentResult.innerText = '';
  interestResult.innerText = '';
}
```

We will call the `resetUI()` function in the event handler before we do anything

```js
function onLoanFormSubmit(e) {
  e.preventDefault();

  resetUI(); // <------ ADD THIS LINE

  //...
}
```
