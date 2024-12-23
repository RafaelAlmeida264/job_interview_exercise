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

**Step 2) Update an airport's data**
To edit the data:

- move the cursor over an item in the list, for example the first one ("LIS, Lisbon Airport");
- click on the icon that corresponds to Edit;
- now type in the new information for this airport: "LIS" for IATA, and "Aeroporto Internacional Humberto Delgado";
- when you confirm, that data has been updated in the list, and if you refresh the browser, you can see that the new data is still there.

**Step 3) Delete an airport**
To delete an airport from the list:

- move the cursor over an item in the list, for example the second one ("LHR, London Heathrow Airport");
- click on the icon that corresponds to Delete;
- a confirmation popup should appear: select "No" if you want to cancel the operation, or select "Yes" to proceed with removing the item from the list.
- selecting "Yes", you can see that the airport has been deleted, the list header is updated and, when you refresh the browser, you can see that only two airports are present (the deleted airport no longer exists).

**[Additional Step] Step 4) Create an airport with an existing IATA**

- create a new airport by typing "ABC" in the IATA input;
- a new alert message written in green should appeared: this message only warns the user that an airport with this respective IATA already exists.

NOTE: Obviously, there is no airport listed with that IATA. In reality, I'm only checking the IATA with a list of hardcoded IATAs (["ABC", "BCD", "CDE"]) and not with the actual list of IATAs of the airports already created. I just wanted to check the design of a warning message (not an error message). In a real situation, if the IATA serves as the unique identifier (ID) of an airport, I assume that you can't create a new airport if that ID already exists. But in this case, I don't prevent the user from creating an airport with a repeated IATA.

**[Additional Step] Step 5) Feedback message**
I created a feedback message (described below in the "Created Components" chapter), but I didn't use it in the application. It is present in the code, inside a comment. I thought it should be important to have something like this when the user successfully completes the creation or deletion of ain airport but I preferred to just follow the exercise script.

To see what the Feedback Message looks like:

- go to the "App.vue" file and remove the comment from the line 12;
- the feedback message will now appear in the browser, under the list of airports, just as I had planned before.
- but since I ended up not using this component, we can leave this line of code as a comment.
