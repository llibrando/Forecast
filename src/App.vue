<template>
  <div>
    <h1>Sales and Stock Forecast</h1>

    <!-- Forecasted Data Display -->
    <h2>Forecasted Data</h2>
    <p><strong>Forecasted Total Sales (USD):</strong> {{ forecastData.totalSales }}</p>
    <p><strong>Forecasted Total Product Stocks (Units):</strong> {{ forecastData.totalStocks }}</p>

    <!-- Sales Chart -->
    <h2>Sales Forecast Chart</h2>
    <canvas id="salesChart" width="400" height="200"></canvas>

    <!-- Stock Chart -->
    <h2>Stock Forecast Chart</h2>
    <canvas id="stockChart" width="400" height="200"></canvas>
  </div>
</template>

<script>
import Chart from 'chart.js/auto';

export default {
  data() {
    return {
      rawData: [
        { date: '2/1/2025', totalSales: 350, totalStocks: 500, totalStocksUsed: 400, stockUsedFood: 200, stockUsedBeverages: 100, stockUsedSnacks: 100 },
        { date: '2/2/2025', totalSales: 400, totalStocks: 450, totalStocksUsed: 380, stockUsedFood: 180, stockUsedBeverages: 120, stockUsedSnacks: 80 },
        { date: '2/3/2025', totalSales: 375, totalStocks: 460, totalStocksUsed: 390, stockUsedFood: 190, stockUsedBeverages: 110, stockUsedSnacks: 90 },
        { date: '2/4/2025', totalSales: 420, totalStocks: 470, totalStocksUsed: 410, stockUsedFood: 210, stockUsedBeverages: 120, stockUsedSnacks: 80 },
        { date: '2/5/2025', totalSales: 380, totalStocks: 480, totalStocksUsed: 370, stockUsedFood: 170, stockUsedBeverages: 130, stockUsedSnacks: 70 },
        { date: '2/6/2025', totalSales: 395, totalStocks: 490, totalStocksUsed: 380, stockUsedFood: 180, stockUsedBeverages: 120, stockUsedSnacks: 80 },
        { date: '2/7/2025', totalSales: 440, totalStocks: 460, totalStocksUsed: 400, stockUsedFood: 200, stockUsedBeverages: 120, stockUsedSnacks: 80 },
        { date: '2/8/2025', totalSales: 460, totalStocks: 470, totalStocksUsed: 420, stockUsedFood: 220, stockUsedBeverages: 130, stockUsedSnacks: 70 },
        { date: '2/9/2025', totalSales: 430, totalStocks: 450, totalStocksUsed: 410, stockUsedFood: 210, stockUsedBeverages: 120, stockUsedSnacks: 80 },
        { date: '2/10/2025', totalSales: 380, totalStocks: 480, totalStocksUsed: 370, stockUsedFood: 180, stockUsedBeverages: 120, stockUsedSnacks: 70 }
      ],
      forecastData: {
        totalSales: 0,
        totalStocks: 0
      },
      salesChart: null,
      stockChart: null
    };
  },
  mounted() {
    this.forecast();
    this.createSalesChart();
    this.createStockChart();
  },
  methods: {
    forecast() {
      // Simple average forecast (can be replaced with more sophisticated methods)
      const totalSalesSum = this.rawData.reduce((sum, item) => sum + item.totalSales, 0);
      const totalStocksSum = this.rawData.reduce((sum, item) => sum + item.totalStocks, 0);

      this.forecastData.totalSales = totalSalesSum / this.rawData.length;
      this.forecastData.totalStocks = totalStocksSum / this.rawData.length;
    },
    createSalesChart() {
      const ctx = document.getElementById('salesChart').getContext('2d');
      this.salesChart = new Chart(ctx, {
        type: 'line',
        data: {
          labels: this.rawData.map(item => item.date),
          datasets: [{
            label: 'Total Sales (USD)',
            data: this.rawData.map(item => item.totalSales),
            backgroundColor: 'rgba(54, 162, 235, 0.2)',
            borderColor: 'rgba(54, 162, 235, 1)',
            borderWidth: 1
          }]
        },
        options: {
          scales: {
            y: {
              beginAtZero: true
            }
          }
        }
      });
    },
    createStockChart() {
      const ctx = document.getElementById('stockChart').getContext('2d');
      this.stockChart = new Chart(ctx, {
        type: 'line',
        data: {
          labels: this.rawData.map(item => item.date),
          datasets: [{
            label: 'Total Stocks (Units)',
            data: this.rawData.map(item => item.totalStocks),
            backgroundColor: 'rgba(255, 99, 132, 0.2)',
            borderColor: 'rgba(255, 99, 132, 1)',
            borderWidth: 1
          }]
        },
        options: {
          scales: {
            y: {
              beginAtZero: true
            }
          }
        }
      });
    }
  }
};
</script>
