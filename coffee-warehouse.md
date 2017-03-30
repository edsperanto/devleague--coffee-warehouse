# Coffee Warehouse API

You've been tasked to build a RESTful API that will help serve and manage data of coffee at a warehouse. Another team will be depending this API in building a front-end application to interact with it.

Draft a routes overview table or list of how you plan on designing your API and submit it to the senior developer for confirmation. 

An example can be found on `buzzword-bingo`: https://github.com/devleague/Buzz-Word-Bingo/blob/master/README.md

We'll be depending on you to build a well-designed RESTful API for our front-end team to work with. Good route naming conventions will be key in providing a simple yet effective API for others to work with. 

## Tables

Build the following (and other) tables and their respective relationships 

### Coffee
- Coffee has a location

### Orders
- An order has a coffee 
- An order has a customer


### Customers
- A customer has an order


## API 

The API should be able to at least do the following... Add more purposeful routes if you feel expands the overall design of the API. 

### Coffee
List all the coffee

Get a coffee by its ID

Get a coffee by its name

List all coffees from the same location

List all coffee with caffiene level below a number

List all coffee with caffiene level above a number

Allow authorized users to post new coffees to the warehouse 

Allow authorized users to alter coffee information 

Allow authorized users to remove coffees 

### Orders
Orders should be able to include customer name that the order is attached to

List all orders 

List an order based by its ID

List all orders that ordered the same coffee

Make a new order

Alter an order

Tag an order pending, shipped, or voided

View all orders that have been tagged pending, shipped, or voided

## Bonus

Allow queries in your routes! Something like `/coffee/search?name="Kona-Kine-Koffee"`