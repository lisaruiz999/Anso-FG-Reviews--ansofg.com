npx create-react-app anso-fg-trading-app
cd anso-fg-trading-app
npm install axios
// server/server.js

const express = require('express');
const cors = require('cors');
const app = express();
const PORT = process.env.PORT || 5000;

app.use(cors());

app.get('/api/stocks', (req, res) => {
  // Sample stock data
  const stocks = [
    { symbol: 'AAPL', name: 'Apple Inc.', price: 150.50 },
    { symbol: 'GOOGL', name: 'Alphabet Inc.', price: 2800.00 },
    { symbol: 'MSFT', name: 'Microsoft Corporation', price: 300.25 }
  ];
  res.json(stocks);
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});

// src/App.js

import React, { useState, useEffect } from 'react';
import axios from 'axios';
import './App.css';

function App() {
  const [stocks, setStocks] = useState([]);

  useEffect(() => {
    axios.get('http://localhost:5000/api/stocks')
      .then(response => {
        setStocks(response.data);
      })
      .catch(error => {
        console.error('Error fetching stock data:', error);
      });
  }, []);

  return (
    <div className="App">
      <header className="App-header">
        <h1>Anso FG Trading App</h1>
        <h2>Available Stocks</h2>
        <ul>
          {stocks.map(stock => (
            <li key={stock.symbol}>
              <strong>{stock.symbol}</strong> - {stock.name} - ${stock.price}
              <button>Buy</button>
              <button>Sell</button>
            </li>
          ))}
        </ul>
      </header>
    </div>
  );
}

export default App;

/* src/App.css */

.App {
  text-align: center;
}

.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 1rem;
}

button {
  margin-left: 0.5rem;
  padding: 0.5rem 1rem;
  background-color: #007bff;
  color: #fff;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

/* src/App.css */

.App {
  text-align: center;
}

.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 1rem;
}

button {
  margin-left: 0.5rem;
  padding: 0.5rem 1rem;
  background-color: #007bff;
  color: #fff;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
