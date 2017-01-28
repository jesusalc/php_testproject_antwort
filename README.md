Test project
===========

Description 
------------
A web application for capturing mailings is to be created.


The user captures broadcasts via a web form. These are stored in a DB.

In addition, a flexibly usable helper class is required, which calculates certain information on the consignment stock (see below). The Helper class itself does not directly access the DB, but receives the broadcasts that are to be considered in the code in the form $helper->addSending (...)

The project consists of the following tasks:
---------------------------------------------------
* Create a suitable DB structure. SQL file to create the DB please store in the folder 'data'. Please use Postgres as DB.
* Create a web form and the required JS code. The use of libraries (eg jQuery, ExtJs, jQueryUI, etc.) is allowed here.
* Create an addSending.php with a function to save the form input in the DB
* Create classes for the send modes. The classes have a save () method, for example, to create the object in the DB. (Functions for loading from the DB do not have to be converted)
* Create the helper class CourierHelper, which can be used to send broadcasts, and which returns various information on the transmitted programs (see below).


Request to the web interface
-------------------------------
Form for recording consignments

* Selection:
  - National package
  - International package
  - Letter national
  - International letter

* Only display other fields if they are necessary (see description of the individual delivery modes)
* The following data is to be collected via the web form: sending type, recipient name, date of receipt, size and weight of the shipment
* Date of receipt as datepicker
* Save by Ajax
* Check with JS that all fields are filled. It is only saved if no data is missing
* After saving Output "Shipment to {recipient} was recorded. Expected delivery on ..., price: ..."

Description of each type of shipment
--------------------------------------------
**Sending Delivery Form**
* Recipient name
* Unique tracking ID
* Date of receipt
* Delivery time 
  - Rules for this:
    - Letters National 1 day, Interational 2 days
    - Packages National 2 days, International 7 days

**International packages (packages and letters)**
* Customs charges
* Country (France, Luxembourg, Belgium)

**Letters**
* Weight in g

**Packages**
* Height, width, length in cm
* Weight in g
* Function to calculate the price

**Prices**
* National package
  - volume <6000 cm2, weight <= 2 kg => 3.95 €
  - volume <6000 cm2, weight> 2 kg => 6.95 €
  - volume> = 6000 => 7.95 €

* International package
  - volume <4000 cm2 -> 6.95
  - volume <6000 cm2, weight <= 2 kg => 8.95 €
  - volume <6000 cm2, weight> 2 kg => 10,95 €

* Brief national
  - Weight <= 100g 0.70 €
  - Weight> 100g => 1,60 €

* International letter
  - Weight <= 100g => 0.90 €
  - Weight> 100g => 2,10 €
  - Weight> = 300g => 4.40 €

**Functions of CourierHelper**
* Function to register a shipment (-> addSending ())
* Function to calculate the total price of all items
* Calculation of how many international consignments, how many national consignments and how many consignments are available
* Calculation of the total weight of the parcels and the total weight of the letters
* Function, which receives a date and shows how many packets are delivered on this day (see delivery period above)

Requirements
------------
* Search the repository and make a pull request after completion.
* Work with several smaller commits, so that we can understand the procedure.
* Data is stored in Postgres DB.
* Do not use external libraries or composer packages for PHP
* JS allows the use of libraries
* Store result in git repository
* Store the SQL file for DB into the data folder