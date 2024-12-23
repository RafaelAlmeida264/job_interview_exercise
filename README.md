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

**Step 2) Update an airport's data **
