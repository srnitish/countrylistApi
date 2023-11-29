import React, { useEffect, useState } from 'react';
import axios from 'axios';

const Countries = () => {
  const [countries, setCountries] = useState([]);

  useEffect(() => {
    const fetchCountries = async () => {
      try {
        const response = await axios.get('https://restcountries.com/v3.1/all');
        const data = response.data;
        setCountries(data);
      } catch (error) {
        console.error('Error fetching countries:', error);
      }
    };

    fetchCountries();
  }, []);

  return (
    <div>
      <h1>Country Name & Currency </h1>
      <ul>
        {countries.map((countryData, index) => (
          
          <li key={index}>
            <p>Country: {countryData.name.common}</p>
            
            {countryData.currencies ? (
              <ul>
                {Object.keys(countryData.currencies).map((currencyData, index) => (
                  <li key={index}>
                    Name: {countryData.currencies[currencyData].name} | Currency: {currencyData} |  Symbol: {countryData.currencies[currencyData].symbol}
                  </li>
                ))}
              </ul>
            ) : (
              <p>No currency information available</p>
            )
            }
          </li>
        ))}
      </ul>
    </div>
  );
};

export default Countries;
