# Payment Dates CSV

This project generates payment dates for the sales department based on certain rules. It provides a web application interface to generate payment dates or you can run a script separately to generate the CSV file directly.

## Requirements
- PHP 8
- Symfony 6
- Composer
- Vue

## Installation and Usage

To run the project:

1. Clone the project repository.
2. Install project dependencies using  `composer install`
3. run `npm install`
4. run `npm run build` 
3. Start the local development server `php -S localhost:8000 -t public`
4. Access the web application in your browser at `http://localhost:8000`.

If you want to generate the CSV file without using the web application, you can run the `GenerateDatesCSV.php` script separately by executing the following command:
`php GenerateDatesCSV.php`
This will generate the CSV file in the same directory where the script exists.
