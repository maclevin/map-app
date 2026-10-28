# Ocean County Boundary Desk

Proof of concept for surveyors doing boundary research in Ocean County, NJ.

- Look up a lot by street address, or by municipality, block and lot
- See the subject lot and its neighbors drawn from the state parcel map
- Get the last deed of record (book and page) for the subject and every adjoiner, with a copyable research list
- Paste a metes-and-bounds description to plot it and check closure, precision and area

## Run it

Open `index.html` in Chrome, Edge, Firefox or Safari. No build step or server. Lookups call the public NJ Office of GIS services directly.

## Data sources

See [docs/data-sources.md](docs/data-sources.md).

Parcel lines are planning-grade, not survey data, and the deed book and page come from the assessment record, which can lag a recent transfer. Confirm against the County Clerk's index.
