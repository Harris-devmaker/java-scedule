# java-scedule
page selectors
// array to store expenses
let expenses = [];

//  to add  expense
function addExpense(description, amount) {
    expenses.push({ description, amount });
}

// display expenses
function displayExpenses() {
    const expenseContainer = document.getElementById('expenseContainer');
    expenseContainer.innerHTML = ''; // Clear previous content

    expenses.forEach(expense => {
        const expenseElement = document.createElement('div');
        expenseElement.classList.add('expense');
        expenseElement.innerHTML = `
            <p><strong>Description:</strong> ${expense.description}</p>
            <p><strong>Amount:</strong> $${expense.amount}</p>
        `;
        expenseContainer.appendChild(expenseElement);
    });
}

// Function to handle form submission
function handleFormSubmit(event) {
    event.preventDefault();
    const description = document.getElementById('description').value;
    const amount = parseFloat(document.getElementById('amount').value);
    if (description && !isNaN(amount)) {
        addExpense(description, amount);
        displayExpenses();
    } else {
        alert('Please enter a valid description and amount.');
    }
}

//  adding expense button
document.getElementById('addExpenseBtn').addEventListener('click', () => {
    const form = `
        <form id="expenseForm">
            <label for="description">Description:</label>
            <input type="text" id="description" required><br>
            <label for="amount">Amount ($):</label>
            <input type="number" id="amount" min="0" step="0.01" required><br>
            <button type="submit">Add Expense</button>
        </form>
    `;
    document.getElementById('expenseContainer').innerHTML = form;
    document.getElementById('expenseForm').addEventListener('submit', handleFormSubmit);
});

// Event listener for view expenses button
document.getElementById('viewExpensesBtn').addEventListener('click', displayExpenses);
