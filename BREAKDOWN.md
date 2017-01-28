# php_testproject_antwort

Test project
===========

description 
------------
* [ ] A web application for capturing mailings is to be created.




The user captures broadcasts via a web form. These are stored in a DB.

In addition, a flexibly usable helper class is required, which calculates certain information on the consignment stock (see below). The Helper class itself does not directly access the DB, but receives the broadcasts that are to be considered in the code in the form $ helper-> addSending (...)

The project consists of the following tasks:
-------------------------------------------------- -
* Create a suitable DB structure. SQL file to create the DB please store in the folder 'data'. Please use Postgres as DB.
* Create a web form and the required JS code. The use of libraries (eg jQuery, ExtJs, jQueryUI, etc.) is allowed here.
* Create an addSending.php with a function to save the form input in the DB
* Create classes for the send modes. The classes have a save () method, for example, to create the object in the DB. (Functions for loading from the DB do not have to be converted)
* Create the helper class CourierHelper, which can be used to send broadcasts, and which returns various information on the transmitted programs (see below).


Request to the web interface

Form for recording consignments

* Selection:
  - National package
  - international package
  - letter national
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








**FRONTEND**
HTML 
1. Webform 
   with Javascript
   with Jquery
   with 




**BACKEND**
PHP
CourierHelper.php
2. addSending.php 
class CourierHelper 
HELPER-KLASS.php
$helper-> addSending
save();

calculateDeliveryTime
calculate





***Functions of CourierHelper***
* Function to register a shipment (-> addSending ())
* Function to calculate the total price of all items
* Calculation of how many international consignments, how many national consignments and how many consignments are available
* Calculation of the total weight of the parcels and the total weight of the letters
* Function, which receives a date and shows how many packets are delivered on this day (see delivery period above)






**LOGIC BACKEND OR FRONTEND**

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







**DB**
3. Postgress


FOLDER 
3. data




ASK Fields: 
--------------
Mailing Project

Liefert deutschlandweit und in viele EU-Länder.Land des *Empfängers Country selectbox

Das Paket ist in der Regel in 1-2 Tagen beim Empfänger
Das Paket ist in der Regel in 5 Tagen beim Empfänger

*Customs charges

Recipient name:  
Unique tracking ID:  
Date of receipt:
Delivery time:

*Brief

*Packet 
Wie groß ist das Paket?

Bitte beachten Sie das maximal zulässige Gewicht von 20 kg und die maximale Länge von 100 cm

Länge
x
Breite
x
Höhe 
cm
Gewicht in g

Sie müssen alle Maße zur Berechnung angeben

[Paketgröße berechnen]


ASK TextFields 
-------------------
Country Selectbox
CustomsCharges Text 
RecipientName Text   --> Empfängername
UniqueTrackingID  Text SelfGenerated
DateOfReceipt SpecialDateBox
DeliveryTime SpecialTimeBox
TypeDelivery Briefe or Packete SelectBox or OptionBox
...Briefe:
  + Gewicht [  ] g Text 
...Pakete:
  + Höhe [ ] cm   Text 
  + Breite [  ] cm   Text 
  + Länge  [  ] cm Text 
  + Gewicht [ ] g Text 




PROCESS
---------


$helper = new HELPER 
$helper->addSending()  
+ addSending.php with function to save form in DB
+ method save()
+ classes for send modes
+ functions for loading from DB do not have to converted
+ CourierHelper.php   used to send broadcasts   ..returns various information on the transmitted programms 

FILES & FOLDERS BE LIKE:

+ addSending.php 
+ CourierHelper.php 
+ data




ASSETS: 

<select name="ctl00$cphContent$selZielLand" onchange="javascript:setTimeout('__doPostBack(\'ctl00$cphContent$selZielLand\',\'\')', 0)" id="ctl00_cphContent_selZielLand" tabindex="215" class="selectStyled">
				<option value="BEL">Belgien</option>
				<option value="BGR">Bulgarien</option>
				<option value="DNK">Dänemark</option>
				<option selected="selected" value="DEU">Deutschland</option>
				<option value="EST">Estland</option>
				<option value="FIN">Finnland</option>
				<option value="FRA">Frankreich</option>
				<option value="GRC">Griechenland</option>
				<option value="GBR">Großbritannien</option>
				<option value="IRL">Irland</option>
				<option value="ITA">Italien</option>
				<option value="HRV">Kroatien</option>
				<option value="LVA">Lettland</option>
				<option value="LTU">Litauen</option>
				<option value="LUX">Luxemburg</option>
				<option value="MCO">Monaco</option>
				<option value="NLD">Niederlande</option>
				<option value="AUT">Österreich</option>
				<option value="POL">Polen</option>
				<option value="PRT">Portugal</option>
				<option value="ROU">Rumänien</option>
				<option value="SWE">Schweden</option>
				<option value="SVK">Slowakei</option>
				<option value="SVN">Slowenien</option>
				<option value="ESP">Spanien</option>
				<option value="CZE">Tschechien</option>
				<option value="HUN">Ungarn</option>

			</select>



            <TimePicker
              key="empfaenger_zeit"
              name="empfaenger_zeit"
              id="empfaenger_zeit"
              hintText="Eingangszeit"
              floatingLabelText="Eingangszeit"
              mode="landscape"
              locale="de"
              hintText="Wählen Sie eine Tageszeit für die Paketlieferung an"
              okLabel="Nutzen"
              cancelLabel="Beenden"
            />


Requirements
--------
* Search the repository and make a pull request after completion.
* Work with several smaller commits, so that we can understand the procedure.
* Data is stored in Postgres DB.
* Do not use external libraries or composer packages for PHP
* JS allows the use of libraries
* Store result in git repository
* Store the SQL file for DB into the data folder