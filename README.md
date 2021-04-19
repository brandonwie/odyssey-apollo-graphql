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

```console
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

---

## Schema defintion language (SDL)

<img src="https://res.cloudinary.com/apollographql/image/upload/e_sharpen:50,c_scale,q_90,w_960,fl_progressive/v1612409235/odyssey/lift-off-part1/type_spacecat_aymp3y_l04j48.jpg" width="100%" alt="Schema Definition Language">

Define a `SpaceCat` type with the following fields: `name` of type `String` (non null), `age` of type `Int`, and `missions` of type List of `Mission`

```typescript
const typeDefs = gql`
  """
  block description
  """
  type SpaceCat {
    "normal description"
    name: String!
    age: Int
    missions: [Mission]
  }
`;
```

## Building our schema

```javascript
const { gql } = require('apollo-server');

const typeDefs = gql`
  type Query {
    "Query to get tracks array for the homepage grid"
    tracksForHome: [Track!]!
  }
  "A track is a group of Modules that teaches about a specific topic"
  type track {
    id: ID!
    "the track's title"
    title: String!
    "the track's main author"
    author: Author!
    "the tracks' main illustration to display in track card or track page detail"
    thumbnail: String
    "the track's approximate length to complete, in minutes"
    length: Int
    "the number of modules this track contains"
    modulesCount: Int
  }

  "Author of a complete Track"
  type Author {
    id: ID!
    "Author's first and last name"
    name: String!
    "Author's profile picture url"
    photo: String
  }
`;

module.exports = typeDefs;
```

## Apollo Server

```javascript
const { ApolloServer, MockList } = require('apollo-server');
const typeDefs = require('./schema');

const mocks = {
  Query: () => ({
    tracksForHome: () => new MockList([6, 9]),
  }),
  Track: () => ({
    id: () => 'track_01',
    title: () => 'Astro Kitty, Space Explorer',
    author: () => {
      return {
        name: 'Grumpy Cat',
        photo:
          'https://res.cloudinary.com/dety84pbu/image/upload/v1606816219/kitty-veyron-sm_mctf3c.jpg',
      };
    },
    thumbnail: () =>
      'https://res.cloudinary.com/dety84pbu/image/upload/v1598465568/nebula_cat_djkt9r.jpg',
    length: () => 1210,
    modulesCount: () => 6,
  }),
};
const server = new ApolloServer({
  typeDefs,
  mocks,
});

server.listen().then(({ url }) => {
  console.log(`
  🚀  Server is running!
  🔉  Listening at ${url}
  📭  Query at https://studio.apollographql.com/dev
  `);
});
```

## React App

```console
📂client
  ┣ 📂src
  ┃ ┣ 📂assets
  ┃ ┣ 📂components
  ┃ ┣ 📂containers
  ┃ ┣ 📂pages
  ┃ ┣ ...
  ┣ ...
```

```javascript
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import GlobalStyles from './styles';
import Pages from './pages';
import { ApolloProvider, ApolloClient, InMemoryCache } from '@apollo/client';

const client = new ApolloClient({
  url: 'http://localhost:4000',
  cache: new InMemoryCache(),
});

ReactDOM.render(
  <ApolloProvider client={client}>
    <GlobalStyles />
    <Pages />
  </ApolloProvider>,
  document.getElementById('root')
);
```

## Defining a query

```javascript
// client/src/pages/tracks.js
import React from 'react';
import { Layout } from '../components';
import { gql } from '@apollo/client';

const TRACKS = gql`
  query getTracks {
    tracksForHome {
      id
      title
      thumbnail
      length
      modulesCount
      author {
        id
        name
        photo
      }
    }
  }
`;

/**
 * Tracks Page is the Catstronauts home page.
 * We display a grid of tracks fetched with useQuery with the TRACKS query
 */
const Tracks = () => {
  return <Layout grid> </Layout>;
};

export default Tracks;
```

\*The resources used in this tutorial are from [Odyssey](https://odyssey.apollographql.com/).
