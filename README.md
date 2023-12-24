import React, { useState } from 'react';
import ExpenseForm from './ExpenseForm';
import ExpenseList from './ExpenseList';

const App = () => {
  const [expenses, setExpenses] = useState([]);
  const [filteredYear, setFilteredYear] = useState('');

  const addExpenseHandler = (expense) => {
    setExpenses((prevExpenses) => [expense, ...prevExpenses]);
  };

  const filterChangeHandler = (selectedYear) => {
    setFilteredYear(selectedYear);
  };

  const filteredExpenses = expenses.filter(
    (expense) => filteredYear === '' || new Date(expense.date).getFullYear().toString() === filteredYear
  );

  return (
    <div>
      <h1>Expense Tracker</h1>
      <ExpenseForm onAddExpense={addExpenseHandler} />
      <div>
        <label>
          Filter by Year:
          <select value={filteredYear} onChange={(e) => filterChangeHandler(e.target.value)}>
            <option value="">All</option>
            <option value="2023">2023</option>
            {/* Add more years as needed */}
          </select>
        </label>
      </div>
      <ExpenseList expenses={filteredExpenses} />
    </div>
  );
};

export default App;
