# Exercise 4: Make it multilingual

In the fourth exercise we will add german (or a language of your choice) as a second language.

## Main Quests overview

1. Add a translation collection
2. Make your menu collection multilingual
3. Dynamically change the languages

## Side quests overview

1. Add another language
2. Use an automatic translator to add more languages on the spot

## Main quests

This one is a bit shorter, but important! We already set everything up nicely in the steps before so we just need to add Accessible labels

### 1. Add a translation collection

We will define our translation table as a collection in the **OnStart** property. Of course we could and should store this information in Dataverse tables in bigger projects.

We will add one row per language and per word/phrase/sentence/paragraph we want to translate.

Each row will look like this: `{id: 1, language: "en", value: "Home"}`

Note: the `id` doesn't necessarily refer to our menu item `id`. In this case it's coincidence.

The complete code we want to add to our **OnStart** looks like this:

```
ClearCollect(colLanguages,
    //english
    {id: 1, language: "en", value: "Home"},
    {id: 2, language: "en", value: "Explore"},
    {id: 3, language: "en", value: "Notifications"},
    {id: 4, language: "en", value: "Messages"},
    {id: 5, language: "en", value: "Lists"},
    {id: 6, language: "en", value: "Bookmarks"},
    {id: 7, language: "en", value: "Twitter Blue"},
    {id: 8, language: "en", value: "Profile"},
    {id: 9, language: "en", value: "More"}

    //german
    {id: 1, language: "de", value: "Startseite"},
    {id: 2, language: "de", value: "Entdecken"},
    {id: 3, language: "de", value: "Mitteilungen"},
    {id: 4, language: "de", value: "Nachrichten"},
    {id: 5, language: "de", value: "Listen"},
    {id: 6, language: "de", value: "Lesezeichen"},
    {id: 7, language: "de", value: "Twitter Blue"},
    {id: 8, language: "de", value: "Profil"},
    {id: 9, language: "de", value: "Mehr"}
);
```

Afterwards we set the current language to english:

```
ClearCollect(colCurrentLanguage,
    Filter(colLanguages, language="en")
);
```

This makes sure we just have the 9 needed english items in our collection `colCurrentLanguage`.

Changing `en` to `de` would result in the 9 german items.

### 2. Make your menu collection multilingual

Now we need to make sure our localized texts end up in our `colMenu`.

We can retrieve a single text with the following piese of code: `LookUp(colCurrentLanguage, id=1, value)`.

Depending on the selected language this is a string that reads `Home` (en) or `Startseite` (de).

This is the code for the whole `colMenu` (exchange it in your **OnStart**):

```
ClearCollect(
    colMenu,
    {id: 1, text: LookUp(colCurrentLanguage, id=1, value), icon: Icon.Home},
    {id: 2, text: LookUp(colCurrentLanguage, id=2, value), icon: Icon.TrendingHashtag},
    {id: 3, text: LookUp(colCurrentLanguage, id=3, value), icon: Icon.Bell},
    {id: 4, text: LookUp(colCurrentLanguage, id=4, value), icon: Icon.Message},
    {id: 5, text: LookUp(colCurrentLanguage, id=5, value), icon: Icon.DetailList},
    {id: 6, text: LookUp(colCurrentLanguage, id=6, value), icon: Icon.Bookmark},
    {id: 7, text: LookUp(colCurrentLanguage, id=7, value), icon: Icon.Diamond},
    {id: 8, text: LookUp(colCurrentLanguage, id=8, value), icon: Icon.Person},
    {id: 9, text: LookUp(colCurrentLanguage, id=9, value), icon: Icon.More}
);
```

### 3. Dynamically change the languages

Now we set an initial language, but we'll want a way to change the language during runtime of our app.

Therefore we create a dropdown to change it:

![dropdown](assets/3_dropdown.gif)

Add a drop down from the insert menu.

As **Items** add `["en", "de"]`.

For the **OnChange** event of the drop down we will repeat the steps from the **OnStart** code.

```
//Set selected language
ClearCollect(colCurrentLanguage,
    Filter(colLanguages, language="en")
);

//Update menu
ClearCollect(
    colMenu,
    {id: 1, text: LookUp(colCurrentLanguage, id=1, value), icon: Icon.Home},
    {id: 2, text: LookUp(colCurrentLanguage, id=2, value), icon: Icon.TrendingHashtag},
    {id: 3, text: LookUp(colCurrentLanguage, id=3, value), icon: Icon.Bell},
    {id: 4, text: LookUp(colCurrentLanguage, id=4, value), icon: Icon.Message},
    {id: 5, text: LookUp(colCurrentLanguage, id=5, value), icon: Icon.DetailList},
    {id: 6, text: LookUp(colCurrentLanguage, id=6, value), icon: Icon.Bookmark},
    {id: 7, text: LookUp(colCurrentLanguage, id=7, value), icon: Icon.Diamond},
    {id: 8, text: LookUp(colCurrentLanguage, id=8, value), icon: Icon.Person},
    {id: 9, text: LookUp(colCurrentLanguage, id=9, value), icon: Icon.More}
);
```

## Side quests

### 1. Add an additional language

Add another language to the collection and drop down.

![ukr](assets/3_ukr.png)



### 2. Use an automatic translator to add more languages on the spot

Works with ChatGPT in one go, try to fully automate it! (Think a little outside the box, using JSON and untyped objects).

Of course feel free to use something different.