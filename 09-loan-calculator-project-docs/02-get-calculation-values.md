# Get Calculation Values

In this lesson, we will bring in the DOM elements that we will be working with and getting the values that we need to do the loan calculation.

Let's start off with selecting what we need from the DOM.

```js
const loanForm = document.getElementById('loan-form'),
  amountInput = document.getElementById('loan-amount'),
  interestInput = document.getElementById('loan-interest'),
  yearsInput = document.getElementById('loan-years'),
  loanResults = document.getElementById('loan-results'),
  monthlyResult = document.getElementById('monthly-result'),
  paymentResult = document.getElementById('payment-result'),
  interestResult = document.getElementById('interest-result'),
  errMsg = document.getElementById('error');
```

Let's add an event listener on to the form and call a function and validate the input.

```js
loanForm.addEventListener('submit', onLoanFormSubmit);
```

```js
function onLoanFormSubmit(e) {
  e.preventDefault();

  // Validate input
  if (
    amountInput.value === '' ||
    interestInput.value === '' ||
    yearsInput.value === ''
  ) {
    alert('Please fill in all fields!');
    return;
  }
}
```

Now let's get the three values that we need to make our calculation. That is the principal, monthly interest and the number of payments (months)

```js
function onLoanFormSubmit(e) {
  e.preventDefault();

  // Validate input
  if (
    amountInput.value === '' ||
    interestInput.value === '' ||
    yearsInput.value === ''
  ) {
    alert('Please fill in all fields!');
    return;
  }

  const principal = parseFloat(amountInput.value);
  const monthlyInterest = parseFloat(interestInput.value) / 100 / 12;
  const numberOfPayments = parseFloat(yearsInput.value) * 12;

  console.log(principal, monthlyInterest, numberOfPayments);
}
```

In the next lesson, we will make the calculation.
