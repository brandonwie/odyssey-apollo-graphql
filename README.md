# Catstronauts (LIFT-OFF PART 1)

Full-stack tutorial from Apollo's new learning platform [Odyssey](https://odyssey.apollographql.com/).

Here is how it'll look like when we're finished
<img src="https://res.cloudinary.com/apollographql/image/upload/e_sharpen:50,c_scale,q_90,w_960,fl_progressive/v1612408870/odyssey/lift-off-part1/Screenshot_2020-12-19_at_18.45.01_yir2f8_fxwozz.png" width="100%" alt="Catstronauts Screenshot">

## Clone the repository

```console
git clone https://github.com/apollographql/odyssey-lift-off-part1 apollographql
```

## Project structure

In `apollographql/`,

```
📦 catstronauts-demo
┣ 📂 client
┃ ┣ 📂 public
┃ ┣ 📂 rc
┃ ┃ ┣ 📂 assets
┃ ┃ ┣ 📂 components
┃ ┃ ┣ 📂 containers
┃ ┃ ┣ 📂 pages
┃ ┃ ┣ 📂 utils
┃ ┃ ┣ 📄 index.js
┃ ┃ ┗ 📄 styles.js
┃ ┣ 📄 README.md
┃ ┣ 📄 package.json
┣ 📂 server
┃ ┣ 📂 src
┃ ┃ ┣ 📄 index.js
┃ ┣ 📄 README.md
┃ ┣ 📄 package.json
┗ 📄 README.md
```

## Install Packages

In both `server/` and `client/` folder:

```console
npm install
```

## Concurrently

Inside `apollographql` folder,

Init npm:

```console
npm init -y
```

Install [concurrently](https://www.npmjs.com/package/concurrently) package:

```console
npm i -D concurrently
```

Add the script below in `package.json`:

```json
"scripts": {
    "start": "concurrently \"cd client && npm start\" \"cd server && npm run start\""
}
```

Ready to run `client/` and `server/` at the same time.

In `apollographql/`:

```console
npm start
```

## Feature Data Requirements

The mockup

<img src="https://res.cloudinary.com/apollographql/image/upload/e_sharpen:50,c_scale,q_90,w_960,fl_progressive/v1612409047/odyssey/lift-off-part1/mockup_rlr38m_dt4zrt.jpg" width="100%" alt="Catstronaut Mockup">

<img src="https://res.cloudinary.com/apollographql/image/upload/e_sharpen:50,c_scale,q_90,w_960,fl_progressive/v1612409106/odyssey/lift-off-part1/card_data_avryfl_pis81f.jpg" width="100%" alt="Catstronauts Track Card Data">

<img src="https://res.cloudinary.com/apollographql/image/upload/e_sharpen:50,c_scale,q_90,w_960,fl_progressive/v1612409160/odyssey/lift-off-part1/LO_02_v2.00_04_53_09.Still002_g8xow6_bbgabz.jpg" width="100%" alt="Catstronauts Data Graph">

## Schema defintion language (SDL)

\*The resources used in this tutorial are from [Odyssey](https://odyssey.apollographql.com/).
