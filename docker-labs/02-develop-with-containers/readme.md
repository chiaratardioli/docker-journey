# Lab 02 — Develop with Containers

## Objective

Learn how Docker can provide a development environment where application changes are reflected immediately.

## What I practiced

* Cloned the official Docker to-do application.
* Started the development environment with Docker Compose.
* Accessed the application in a browser.
* Modified the backend greeting.
* Changed the frontend placeholder text and background color.
* Observed changes without manually rebuilding the application.

The official tutorial uses a React frontend, a Node.js backend, MySQL, and other supporting services. <Cite ref="turn0view0" />

## Commands

```bash
git clone https://github.com/docker/getting-started-todo-app
cd getting-started-todo-app
docker compose watch
```

I open the application at:

http://localhost

## Screenshots

### Application running

![Application running](./images/01-01-app-running.md)

### Backend change

I modified the file `backend/src/routes/getGreeting.js`:
```js
const GREETINGS = [
  "Whalecome!",
  "All hands on deck!",
  "Charting the course ahead!",
];

module.exports = async (req, res) => {
  res.send({
    greeting: GREETINGS[Math.floor(Math.random() * GREETINGS.length)],
  });
};
```
![Backend change: Updated greeting](./images/01-02-updated-greeting.md)

### Frontend change

I modified the `placeholder` attribute of the `Form.Control` element contained the file `client/src/components/AddNewItemForm.jsx`:
```jsx
<Form.Control
  value={newItem}
  onChange={(e) => setNewItem(e.target.value)}
  type="text"
  placeholder="What do you need to do?"
  aria-label="New item"
/>
```

I adjusted the background-color attribute in the `client/src/index.scss` file:
```sass
@import 'bootstrap/scss/bootstrap';

body {
    background-color: #25bfbc;
    margin-top: 50px;
    font-family: 'Lato';
}
```
![Frontend change: Updated placeholder and color background](./images/01-03-updated-placeholder-background.md)

## What I learned

Docker Compose can start multiple services together, while `docker compose watch` helps synchronize local changes with the running development environment.
