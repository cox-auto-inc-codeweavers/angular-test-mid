# Technical Test

### Midlevel Software Engineer, Frontend

**Goal**: Implement features for a Vehicle Inventory and Finance Calculator.

**Scenario**:
You are tasked with building a Vehicle listing and Finance Details view feature for an automotive finance web application. The application needs to display a list of retailers available vehicles, allow users to filter and sort these vehicles, and then view the details of a single vehicle along with a representative finance calculation on a separate page.

**Delivery**

Please fork the repo and provide a URL to your own solution

**Instructions:**

1. You will be provided with a basic Angular CLI project that includes a pre-configured environment and mock data.
2. Your primary goal is to implement the functionality described below. The focus should be on clean code, best practices, and effective use of Angular and RxJS patterns.
3. Assume the existence of an external API for vehicle data and finance terms. Simulate API calls using `setTimeout` to mimic asynchronous behaviour and provided mock data.
4. If you encounter any assumptions you need to make, please state them clearly.
5. There is no style guide for this test, the interface and look and feel however you like, but should be accessible and usable.
6. Please allow at least 60 minutes for this test

## Tasks

**1. Data Model & Service**

- Define an Interface: Create a TypeScript interface for a `Vehicle` object that matches the example data provided
- Implement an injectable `VehicleService` that includes two methods:
  - Return an `Observable` containing all of the mock `Vehicle` data
  - Return an `Observable` of a single `Vehicle` from the mock `Vehicle` data based on a provided ID.
- The `VehicleService` methods must simulate an asynchronous API call

**2. Vehicle List Component**

- Create a component which fetches Vehicles and displays them in a list
  - Ensure proper `Observable` handling using the `async` pipe
  - Use `trackBy` with `*ngFor` for improved performance
- Add an input field to the component
  - Implement filtering logic using Reactive Forms and RxJs operators, the user should be able to filter on make and model
- Add a dropdown or buttons for sorting the Vehicles (e.g. by `price`, `year`, or `mileage` ascending and descending)
  - Implement the sorting logic using RxJs operators and JavaScript array methods
- Each vehicle in the list should have a clickable element that navigates to its corresponding detail view. Use the vehicles `id` as a route parameter

**3. Vehicle Detail Component**

- Configure correct routing for the component (`/vehicles/:id`)
- Fetch and display the correct details (`make`,`model`,`year`,`price`,`mileage`,`colour`) for the vehicle with the corresponding `id`
- Handle cases where the vehicle could not be fetched

**4. Finance Calculator Service**

- Create an injectable `FinanceCalculator` service with a method that accepts a `Vehicle`, `term`, and `deposit` which returns an `Observable` containing a `FinanceQuote`.

```
interface FinanceQuote {
    onTheRoadPrice: number;
    totalDeposit: number;
    totalAmountOfCredit: number;
    numberOfMonthlyPayments: number;
    monthlyPayment: number;
}
```

- Each property can be worked out as follows:
  - **onTheRoadPrice**: The Vehicle price
  - **totalDeposit**: The provided Deposit amount
  - **totalAmountOfCredit**: Subtract the Deposit from the Vehicle Price
  - **numberOfMonthlyPayments**: The provided term
  - **monthlyPayment**: The total amount of credit divided by the term

**5. Vehicle Detail Component**

- Present a default finance calculation for the displayed vehicle. Follow consistent practice used for retrieving `Vehicle` data for the Finance Calculation. The deposit can be hardcoded to 10% of the Vehicle price in this instance, and term can be defaulted to 60 months.
- Create an UI for the user to provide a `term` and `deposit` to the `FinanceCalculatorService`, update the results accordingly.

**6. Code Review**

- Take a moment to review your code, ensure you are using best practices for TypeScript (interfaces, enums if applicable, strong typing)
- Ensure you are using Angular best practices, and all `Observables` are handled appropriately
- Ensure errors are handled gracefully
- Ensure your code is clean, readable, and well organised
