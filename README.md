# airtable-client

**A lightweight, general-purpose Kotlin client for the [Airtable API](https://airtable.com/api).**

⚠️ This library is under active development. The API may change before reaching version 1.0.

## Installation

After cloning it from a repository, you need to publish the library into your local maven repository.

```
> gradlew publishToMavenLocal
```

After publishing you can add the library as a dependecy into your local gradle file:

```kotlin
//...
repositories {
  mavenLocal() // or your own Maven repo
  mavenCentral()
}

dependencies {
  implementation("com.moon42.airtable:airtable-client:0.0.2")
}
//...
```

## Usage

First, you have to initialize the client with a base ID and an airtable token. 

```kotlin
fun main() {
    val client = AirtableClient(baseId = "your-base-id", apiKey = "your-api-key")
    val records = client.fetchAirtableData(
        tableId = "your-table-id", 
        filterFormula = null,
        targetClass = MyDataClass::class.java)
    println(records)
}
```

After you can read any table data and deserialize it into objects with ``fetchAirtableData``. For now it reads **all data** from the given table so use it carefully.

Information about how you can get an airtable base id or table id can be found [here](https://support.airtable.com/docs/finding-airtable-ids#finding-base-table-and-view-ids-from-urls).

[Here](https://support.airtable.com/docs/creating-personal-access-tokens) you can find how to create an access token to Airtable API.

[Reference](https://support.airtable.com/docs/airtable-web-api-using-filterbyformula-or-sort-parameters) of using filter formulas in Airtable API.

The data fetched from Airtable will be deserialized into instances of ``targetClass`` using [GSON](https://github.com/google/gson).  