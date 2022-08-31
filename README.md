# nominatim-rs
API bindings for the reverse geocoding API.

## Examples
**Create a client:**
```rust no_run
let client = Client::new(IdentificationMethod::from_user_agent(
    "Example Application Name",
));
```

**Check the server's status:**
```rust no_run
let status = client.status().await.unwrap();

println!("{}", client.status().await.unwrap());
```

Returns:
```
OK
```

**Search for some places with just a simple query:**
```rust no_run
let search_results = client.search("statue of liberty").await.unwrap();

for place in search_results {
    println!("{}", place.display_name);
}
```

Returns:
```
Statue of Liberty, Flagpole Plaza, Manhattan Community Board 1, Manhattan, New York County, City of New York, New York, 10004, United States
Statue of Liberty, North Center Street, Plymouth, Marshall County, Indiana, 46563, United States
Statue of Liberty, Visnesvegen, Visnes, Karmøy, Rogaland, 4264, Norge
Statue of Liberty, East Grace Street, Chimborazo, Church Hill, Richmond, Virginia, 23298, United States
Statue of Liberty, East 12th Street, Des Moines, Polk County, Iowa, 50316, United States
Statue of Liberty, Locust Street, Cathedral Historic District, Dubuque, Dubuque County, Iowa, 52001, United States
Statue of Liberty, IA 946, South Port, Dubuque, Dubuque County, Iowa, 52001, United States
Statue of Liberty, Colorado Avenue, La Junta, Otero County, Colorado, 81050, United States
Statue of Liberty, North Main Street, Leon, Decatur County, Iowa, 50144, United States
Statue of Liberty, 23501, Macedonia Road, Hegar, Hockley, Waller County, Texas, 77447, United States
```

**Get the closest place to a latitude and longitude pair:**
```rust no_run
let reverse_search = client
    .reverse("40.689249", "-74.044500", None)
    .await
    .unwrap();

println!("{}", reverse_search.display_name);
```

Returns:
```
Statue of Liberty, Flagpole Plaza, Manhattan Community Board 1, Manhattan, New York County, City of New York, New York, 10004, United States
```

**Lookup places from a list of OSM Node, Way, or Relations:**
```rust no_run
let lookup_results = client.lookup(vec!["R146656", "W50637691"]).await.unwrap();

for place in lookup_results {
    println!("{}", place.display_name);
}
```

Results:
```
Manchester, Greater Manchester, England, United Kingdom
Brandenburger Tor, Brandenburger Straße, Historische Innenstadt, Innenstadt, Potsdam, Brandenburg, 14467, Deutschland
```

## License
```
MIT License

Copyright (c) 2022 Grant Handy

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
