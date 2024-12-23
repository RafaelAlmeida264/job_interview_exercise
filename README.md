# Job Interview Exercise

This is my resolution of the exercise I was asked to do after the job interview.<br>
It's a simple application with a list of airports, where we can create new airports, listing them, updating their data and deleting them from the list (CRUD operations.)

This file contains the process of running the application, its functionalities, and a complete description of the steps I followed from the first sketches to the creation of the application.

This project was developed using [Vue 3](https://vuejs.org/guide/quick-start.html) in [Vite](https://vite.dev/config/).

## Recommended IDE Setup

Download or clone this project to your computer.
<br>Open the project folder using your preferred IDE.Personally, I used [Visual Studio Code](https://code.visualstudio.com/).

<!--
[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).
-->

<!--
## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).
-->

## Project Setup

Versions used during this project:<br>
npm: 10.9.2<br>
Node.js: v20.13.1

To install the latest version of npm, please type the following command in the terminal:

```sh
npm install -g npm@latest
```

<!--
### Compile and Hot-Reload for Development
-->

To run this project, while inside the directory of the project, use the following command:

```sh
npm run dev
```

<!--
### Compile and Minify for Production

```sh
npm run build
```
-->

## Project Description

The application displays a list of airports and a button to add a new airport to the list. A list is made up of several airports (each airport corresponds to a different item). When you want to add a new airport or update the data of an airport that has already been created, a popup appears with a form to fill in. When you want to delete an airport from the list, a small confirmation popup appears before the airport is removed.<br>

All these operations (Create, Read, Update and Delete) are working.

### How to Use this App (Testing)

**Step 0) Initial look of the application**<br>
As soon as the application starts, you can see a button to insert a new airport and the header of the list of airports. Since there is no airport created (and saved in LocalStorage), the list will not show any airports and the header should say that there are "0 Airports listed".

**Step 1) Create a new airport**<br>
To create a new airport:

- click on the "Insert New Airport" button;
- type the following data into the form: "LIS" for the IATA and "Lisbon Airport" for the Airport Name;
- click on the "Confirm" button to create a new airport;
- the new airport will now appear listed and the list header will have its information updated ("1 Airport listed").

To test data validation on the form:

- click on the "Insert New Airport" button;
- this time, leave both inputs empty;
- click on the "Confirm" button: three error messages should appear;
- type "123" in IATA: the message about the length of the string should not appear;
- type "LH" in IATA: the alphabetic character message should not appear;
- type "LHR" in IATA: only the message about both parameters being mandatory is shown;
- type "London Heathrow Airport" in the Name input and confirm: a new airport is added to the list and the list header is now updated.

Finally, create a new aiport just so we have three listed airports (IATA: "OPO", Name: "Francisco Sá Carneiro Airport"). You can refresh the page in your browser to see that those three airports are still listed (since they are saved and retrieved from LocalStorage).

**Step 2) Update an airport's data**<br>
To edit the data:

- move the cursor over an item in the list, for example the first one ("LIS, Lisbon Airport");
- click on the icon that corresponds to Edit;
- now type in the new information for this airport: "LIS" for IATA, and "Aeroporto Internacional Humberto Delgado";
- when you confirm, that data has been updated in the list, and if you refresh the browser, you can see that the new data is still there.

**Step 3) Delete an airport**<br>
To delete an airport from the list:

- move the cursor over an item in the list, for example the second one ("LHR, London Heathrow Airport");
- click on the icon that corresponds to Delete;
- a confirmation popup should appear: select "No" if you want to cancel the operation, or select "Yes" to proceed with removing the item from the list.
- selecting "Yes", you can see that the airport has been deleted, the list header is updated and, when you refresh the browser, you can see that only two airports are present (the deleted airport no longer exists).

**[Additional Step] Step 4) Create an airport with an existing IATA**

- create a new airport by typing "ABC" in the IATA input;
- a new alert message written in green should appeared: this message only warns the user that an airport with this respective IATA already exists.

NOTE: Obviously, there is no airport listed with that IATA. In reality, I'm only checking the IATA with a list of hardcoded IATAs (["ABC", "BCD", "CDE"]) and not with the actual list of IATAs of the airports already created. I just wanted to check the design of a warning message (not an error message). In a real situation, if the IATA serves as the unique identifier (ID) of an airport, I assume that you can't create a new airport if that ID already exists. But in this case, I don't prevent the user from creating an airport with a repeated IATA.

**[Additional Step] Step 5) Feedback message**<br>
I created a feedback message (described below in the "Created Components" chapter), but I didn't use it in the application. It is present in the code, inside a comment. I thought it should be important to have something like this when the user successfully completes the creation or deletion of ain airport but I preferred to just follow the exercise script.

To see what the Feedback Message looks like:

- go to the "App.vue" file and remove the comment from the line 12;
- the feedback message will now appear in the browser, under the list of airports, just as I had planned before.
- but since I ended up not using this component, we can leave this line of code as a comment.

### Created Components

For this application, I created the following components:

- Button.vue:
  There are three types of buttons in the application: a button with icon (used to add a new aiport to the list), a primary action button (used to confirm the creation of a new airport, to confirm the update of data for a specific airport, or to cancel the request to delete an airport), and a secondary action button (used to cancel the request to create an airport or update its data, or to confirm the request to delete an airport).

- Form.vue:
  There are two types of forms: one for creating an airport and another for updating an airport's data. The only difference between them is the tile, "Insert New Airport" and "Update Airport Data", and the fact that I supply an airport (from the list of airports) when I need to update its information.<br>
  The form has two inputs, one for IATA and one for Name. It also has two buttons, one to cancel and one to confirm the operation. Finally, it has its own area to list all the error messages when validating the data.<br>
  With regard to the error messages, I chose to show them only after the user clicks the "Confirm" button for the first time. After that, they appear and disappear as the user types something into the input boxes. Out of personal preference, I don't think it would be right to show the error messages as soon as the user opens the popup and/or starts typing something.<br>
  I confess that I didn't do something I would have liked to have done: although the data update is working, when the popup is opened it doesn't show the user the old data for the respective airport. That said, the user is obliged to enter all the data (although in this case there are only two) if they only want to change one of them - which shouldn't happen!

- List.vue:
  The list has a header with the number of airports created, and a list with as many items as there are airports. When creating a new list, I provide the list of airports already created (or an empty list if none exists yet) stored in LocalStorage.

- ListItem.vue:
  A list item corresponds to an airport with two pieces of information (IATA and Name), separated by a comma. When creating a new item, I supply an airport from the list of airports (which already contains the required data). When the cursor hovers an item, it is highlighted and displays two new buttons, one to edit the information of the respective airport, and the other to delete it from the list.

- DeletePopup.vue:
  This popup is just a Yes/No form with two buttons to confirm/cancel the request to delete a selected airport.

- Feedback.vue:
  Note: I created this sixth component as something additional to what was requested in the exercise. However, it is not executed during the application. I believe there should be an alert message (in shades of green, for example) when the user successfully completes the creation of a new airport and when they remove an airport from the list. Likewise, when something goes wrong, a similar message (in shades of red) should also appear (this last design is not present in the code).
