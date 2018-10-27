# algolia-firestore-sync
Simple helper for syncing indices to Firestore on Firebase


## Usage

```
const functions = require('firebase-functions');
const algoliasearch = require('algoliasearch');
const algoliaSync = require('algolia-firestore-sync');

const algolia = algoliasearch(functions.config().algolia.appid, functions.config().algolia.adminkey);
const index = algolia.initIndex('ingredients');

exports.syncIngredients = functions.firestore.document('/<CollectionName>/{id}').onWrite(
  (change, context) => {
    return algoliaSync.syncAlgoliaWithFirestore(index, change, context)
  }
);
```