# v-clothingflags

Restriction tags of GTA V freemode ped clothing items.

Some items have no data, which means they might be the initial freemode ped clothes (aka non-DLC clothes) OR Rockstar just didn't give them any restriction tags.

Visit https://wiki.rage.mp/index.php?title=Clothes for a list of clothes.

# JS Example

```js
const maleComponentTags = require("./male_component_tags");
const malePropTags = require("./male_prop_tags");
const femaleComponentTags = require("./female_component_tags");
const femalePropTags = require("./female_prop_tags");

function isHatAHelmet(gender, hatDrawable, hatTexture) {
    gender = gender.toLowerCase();

    const tags = gender === "male" ? malePropTags : gender === "female" ? femalePropTags : undefined;
    if (tags === undefined || tags[0][hatDrawable] === undefined || tags[0][hatDrawable][hatTexture] === undefined) {
        return false;
    }

    return tags[0][hatDrawable][hatTexture].includes("HELMET");
}

function getClothingFlags(gender, componentIndex, topDrawable, topTexture) {
    gender = gender.toLowerCase();

    const tags = gender === "male" ? maleComponentTags : gender === "female" ? femaleComponentTags : undefined;
    if (tags === undefined || tags[componentIndex] === undefined || tags[componentIndex][topDrawable] === undefined || tags[componentIndex][topDrawable][topTexture] === undefined) {
        return [];
    }

    return tags[componentIndex][topDrawable][topTexture];
}

/*
    Check if these are a helmet:
    Male hat #45 - https://wiki.rage.mp/images/e/ec/Prop_M_0_45.jpg
    Male hat #70 - https://wiki.rage.mp/images/6/60/Prop_M_0_70.jpg
    Female hat #36 - https://wiki.rage.mp/images/e/e7/Prop_F_0_36.jpg
    Female hat #116 - https://wiki.rage.mp/images/3/38/Prop_F_0_116.jpg
 */
console.log(isHatAHelmet("male", 45, 0)); // Output: false
console.log(isHatAHelmet("male", 70, 0)); // Output: true
console.log(isHatAHelmet("female", 36, 0)); // Output: false
console.log(isHatAHelmet("female", 116, 0)); // Output: true

/*
    Get the flags of:
    Male top #311 - https://wiki.rage.mp/images/7/78/Clothing_M_11_311.jpg
    Female top #322 - https://wiki.rage.mp/images/4/45/Clothing_F_11_322.jpg
 */
console.log(getClothingFlags("male", 11, 311, 0)); // Output: ['CASINO_ITEM', 'JACKET', 'TUX_JACKET', 'OPEN_JACKET']
console.log(getClothingFlags("female", 11, 322, 0)); // Output: ['CASINO_ITEM', 'DRESS', 'HIPSTER_DRESS']
```