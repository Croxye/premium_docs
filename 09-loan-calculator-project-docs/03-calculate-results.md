# Calculate Results

In this lesson, we will take the principal, monthly interest and number of payments and calculate the monthly payment and total interest.

Let's create the function that will calculate the results.

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
    alert('Please check your numbers');
    return;
  } else {
    console.log('Success');
  }
}
```

Make sure that you call the function in the `onLoanFormSubmit` function.

```js
function onLoanFormSubmit(e) {
  //...

  calculateResults(principal, monthlyInterest, numberOfPayments); // <------ ADD THIS LINE
}
```

Again, you don't really need to understand the formula. You just need to know where to look to find what you need and then implement it so that you plug the correct values into it.

Here are 2 resources that helped me understand the formula:

- https://www.kasasa.com/blog/how-to-calculate-loan-payments-in-3-easy-steps
- https://gist.github.com/letrongtanbs/d29354da30f12784bc8453af4e4fb6ff

After calculating the results, we need to display them on the page, we checked the `monthly` value and made sure it was a number. If it is, we are just console logging success. In the next lesson, we will show the spinner and the results on the page.
